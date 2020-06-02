### MyBatis 把SQL作为参数

#### 1. XxMapper.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="xx.xx.xx.xx.XxMapper">
  <select id="selectBySql" parameterType="java.util.Map" resultType="java.util.HashMap">
    <![CDATA[ ${sql} ]]>
  </select>
</mapper>
```

#### 2. XxMapper.java

```java
@Mapper
public interface XxMapper {
    List<Map<String, Object>> selectBySql(Map<String, Object> params);
}
```

#### 3. 调用

```java
Map<String,Object> params = new HashMap<>();
params.put("sql","select count(*) from user where code like #{code}");
params.put("code","1%");
List<Map<String, Object>> maps = xxMapper.selectBySql(params);
```