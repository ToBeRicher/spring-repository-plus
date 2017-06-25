# spring-repository-plus
https://github.com/ZhongjunTian/spring-repository-plus
This is actually a good implementation of spring JPA Specification interface, it makes front-end having full control of filtering data with very little back-end code.

Querying with spring-repository-plus is as simple as:


![](http://upload-images.jianshu.io/upload_images/6110329-0cf77a8569a20c56.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

or

![](http://upload-images.jianshu.io/upload_images/6110329-52fc3da8a7b2eb08.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Here is **ALL** your back-end code
```
    @PostMapping("/persons")
    public List<Person> filter(@RequestBody Filter filter){
        return selectFrom(personRepository).leftJoin("address").where(filter).findAll();
    }
```
```
    public interface PersonRepository extends JpaRepository<Person, Long>,JpaSpecificationExecutor {
    }
```
But with such little code, you can also filter data by **ANY** complex logic (and, or) and **ANY** operations (equal, startswith, endswith, greaterthan...)

The example below is equivalent to 
lastName='Tian' AND (address.city='Dallas' OR address.city like 'San%')

![](http://upload-images.jianshu.io/upload_images/6110329-7ddd70b1687f6900.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

or

![](http://upload-images.jianshu.io/upload_images/6110329-cf58162836cbae40.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

Table definition
```
CREATE TABLE PERSON (
	id BIGINT GENERATED BY DEFAULT AS IDENTITY,
	first_name varchar(255) not null,
	last_name varchar(255) not null,
	address_id int null
);
CREATE TABLE ADDRESS (
	id BIGINT GENERATED BY DEFAULT AS IDENTITY,
	city varchar(255) not null
);
```

***And please feel free to give me any advice.***

## User guide  
### clone and run  

git clone https://github.com/ZhongjunTian/spring-repository-plus.git   
cd spring-repository-plus  
mvn spring-boot:run  

You can look at PersonControllerTest.java and TestEntityControllerTest.java for more details,
