---
layout: post_layout
comments: true
title:  "SpringData Mongodb converting problem"
excerpt: "Way to solve SpringData Mongodb problem of object converting from DBObjects to POJO."
date:   2017-05-04 11:00:00
mathjax: false
---


<p>
The reason causes this problem is lacking of some converter in spring data project, in this case a converter of converting from Date to Timestamp is missing.
<br/>
We will fix this problem by adding a DateToTimestamp converter, which just simply takes three moves, here we go:
</p>
### 1. We need to build a converter like this:
```java
package com.ewandian.thirdparty.docking.facade.converter;

import org.apache.commons.beanutils.ConversionException;
import org.springframework.core.convert.converter.Converter;

import java.sql.Timestamp;
import java.util.Date;

/**
 * Created by suhd on 2017-03-28.
 */
public class DateToTimestampConverter implements Converter<Date, Timestamp> {

    public DateToTimestampConverter() {
    }

    public Timestamp convert(Date date) {
        try {
            return new Timestamp(date.getTime());
        } catch (Exception e) {
            throw new ConversionException("Error converting Date to Timestamp");
        }
    }

}
```
### 2. A MappingMongoConverter, it's a stateless object, converters injecting through construct-arg.
```java
package com.ewandian.thirdparty.docking.facade.converter;

import org.springframework.core.convert.converter.Converter;
import org.springframework.data.mapping.context.MappingContext;
import org.springframework.data.mongodb.core.convert.CustomConversions;
import org.springframework.data.mongodb.core.convert.DbRefResolver;
import org.springframework.data.mongodb.core.convert.MappingMongoConverter;
import org.springframework.data.mongodb.core.mapping.MongoPersistentEntity;
import org.springframework.data.mongodb.core.mapping.MongoPersistentProperty;

import java.util.List;

/**
 * Created by suhd on 2017-03-28.
 */
public class EwdMappingMongoConverter extends MappingMongoConverter {

    public EwdMappingMongoConverter(DbRefResolver dbRefResolver, MappingContext<? extends MongoPersistentEntity<?>, MongoPersistentProperty> mappingContext, List<Converter> converters) {
        super(dbRefResolver, mappingContext);
        super.setCustomConversions(new CustomConversions(converters));
        super.afterPropertiesSet();
    }

}
```
### 3. Configuration of Spring XML
```java
<bean id="simpleMongoDbFactory" class="org.springframework.data.mongodb.core.SimpleMongoDbFactory"
	  c:mongo-ref="mongo" c:databaseName="${mongo.database}"/>

<bean id="defaultDbRefResolver" class="org.springframework.data.mongodb.core.convert.DefaultDbRefResolver">
	<constructor-arg name="mongoDbFactory" ref="simpleMongoDbFactory"></constructor-arg>
</bean>

<bean id="mongoMappingContext" class="org.springframework.data.mongodb.core.mapping.MongoMappingContext">
</bean>

<bean id="ewdMappingMongoConverter" class="com.ewandian.thirdparty.docking.facade.converter.EwdMappingMongoConverter">
	<constructor-arg name="dbRefResolver" ref="defaultDbRefResolver"></constructor-arg>
	<constructor-arg name="mappingContext" ref="mongoMappingContext"></constructor-arg>
	<constructor-arg name="converters">
		<list>
			<bean class="com.ewandian.thirdparty.docking.facade.converter.DateToTimestampConverter"></bean>
		</list>
	</constructor-arg>
</bean>

<bean id="mongoTemplate" class="org.springframework.data.mongodb.core.MongoTemplate">
	<constructor-arg name="mongoDbFactory" ref="simpleMongoDbFactory"></constructor-arg>
	<constructor-arg name="mongoConverter" ref="ewdMappingMongoConverter"></constructor-arg>
</bean>
```
