### MyBatis 批量操作

#### 批量插入

```xml
<insert id="insertBatch" parameterType="java.util.List">
	INSERT INTO user
	(
	`code`,
	`name`,
	`created_time`,
	`created_user`,
	`modified_time`,
	`modified_user`
	)
	values
	<foreach collection="list" item="info" separator=",">
	    (
	    #{info.code},
	    #{info.name},
	    now(),
	    #{info.createdUser},
	    now(),
	    #{info.modifiedUser}
	    )
	</foreach>
</insert>
```

```xml
<insert id="batchInsertB2B" parameterType="java.util.List">
	INSERT INTO user
	(
	`code`,
	`name`,
	`created_time`,
	`created_user`,
	`modified_time`,
	`modified_user`
	)
	<foreach collection="list" item="info" separator="union all">
	SELECT
	    #{info.code},
	    #{info.name},
	    now(),
	    #{info.createdUser},
	    now(),
	    #{info.modifiedUser}
	</foreach>
</insert>
```

#### 批量删除

```xml
<delete id="deleteBatch" parameterType="java.util.List">
	delete user
	where code in 
	<foreach collection="codes" item="codeItem" open="(" close=")" separator=",">
	#{codeItem}
	</foreach>
</delete>
```

#### 查询

```xml
<select id="select" parameterType="java.util.List" resultMap="Map">
	select
		`code`,
		`name`,
		`created_time`,
		`created_user`,
		`modified_time`,
		`modified_user`
	from user
	where `code` in
	<foreach collection="codes" item="codeItem" open="(" close=")" separator=",">
		#{codeItem}
	</foreach>
</select>
```
