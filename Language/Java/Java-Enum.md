### Java 枚举

#### 遍历枚举

```java
import java.util.Arrays;

/**
 * @description: 遍历枚举
 * @author: jiaxiaojiao
 * @create: 2020-06-01 17:11
 */
public enum AlarmGrade {
    ATTENTION("attention", "提示"),
    WARNING("warning", "警告"),
    SERIOUS("serious", "严重"),
    FAULT("fault", "故障"),
    UNKNOWN("unknown", "未知");

    private String code;
    private String message;


    AlarmGrade(String code, String message) {
        this.code = code;
        this.message = message;
    }

    /**
     * @description: 获取枚举-普通for循环遍历
     * @Param: code
     * @return: AlarmGrade
     */
    public static AlarmGrade getEnum(String code) {
        AlarmGrade[] alarmGrades = AlarmGrade.values();
        for (int i = 0; i < alarmGrades.length; i++) {
            if (alarmGrades[i].code.equals(code)) {
                return alarmGrades[i];
            }
        }
        return AlarmGrade.UNKNOWN;
    }

    /**
     * @description: 获取枚举-增强for循环遍历
     * @Param: code
     * @return: AlarmGrade
     */
    public static AlarmGrade getEnum2(String code) {
        for (AlarmGrade alarmGrade : AlarmGrade.values()) {
            if (alarmGrade.code.equals(code)) {
                return alarmGrade;
            }
        }
        return AlarmGrade.UNKNOWN;
    }

    /**
     * @description: 获取枚举-Lambda表达式遍历
     * @Param: code
     * @return: AlarmGrade
     */
    public static AlarmGrade getEnum3(String code) {
        return Arrays.asList(AlarmGrade.values()).stream()
                .filter(alarmGrade -> alarmGrade.code.equals(code))
                .findFirst().orElse(AlarmGrade.UNKNOWN);
    }
}

```


### 参考
* https://www.cnblogs.com/miracle-luna/p/10995539.html