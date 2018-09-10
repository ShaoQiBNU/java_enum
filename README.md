Java enum枚举类的用法
====================

# 一. enum类基本用法
> java枚举类是一组预定义常量的集合，使用enum关键字声明这个类，常量名称官方建议大写。下面看一个具体实例：

## 1.定义一个枚举类，采用switch遍历

```java
public class EnumTest {
    Day day;
    
    public EnumTest(Day day) {
        this.day = day;
    }

    public void tellItLikeItIs() {
        switch (day) {
            case MONDAY:
                System.out.println("周一各种不在状态");
                break;
            case FRIDAY:
                System.out.println("周五感觉还不错");
                break;
            case SATURDAY: case SUNDAY:
                System.out.println("周末给人的感觉是最棒的");
                break;
            default:
                System.out.println("周内的感觉就那样吧。。。");
                break;
        }
    }

    public enum Day {
        SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
    }

}
```

## 2. Main函数调用

```java
public class Main {

    public static void main(String[] args) {
	EnumTest firstDay = new EnumTest(EnumTest.Day.SUNDAY);
	firstDay.tellItLikeItIs();

    EnumTest thirdDay = new EnumTest(EnumTest.Day.WEDNESDAY);
    thirdDay.tellItLikeItIs();

    EnumTest fifthDay = new EnumTest(EnumTest.Day.FRIDAY);
    fifthDay.tellItLikeItIs();

    EnumTest sixthDay = new EnumTest(EnumTest.Day.SATURDAY);
    sixthDay.tellItLikeItIs();

    EnumTest seventhDay = new EnumTest(EnumTest.Day.SUNDAY);
    seventhDay.tellItLikeItIs();

    }
}
```




# 二. enum类自定义属性

> enum类可以赋予每一个枚举值若干个属性，例如：

## 1. enum定义
```java
public class EnumTest2 {
    Day day;

    public EnumTest2(Day day) {
        this.day = day;
    }

    public void tellItLikeItIs() {
        switch (day) {
            case MONDAY:
                System.out.println(day.getName()+day.getValue());
                break;

            case FRIDAY:
                System.out.println(day.getName()+day.getValue());
                break;

            case SATURDAY: case SUNDAY:
                System.out.println(day.getName()+day.getValue());
                break;

            default:
                System.out.println(day.getName()+day.getValue());
                break;
        }
    }

    public enum Day {
        MONDAY(1, "星期一", "星期一各种不在状态"),
        TUESDAY(2, "星期二", "星期二依旧犯困"),
        WEDNESDAY(3, "星期三", "星期三感觉半周终于过去了"),
        THURSDAY(4, "星期四", "星期四期待这星期五"),
        FRIDAY(5, "星期五", "星期五感觉还不错"),
        SATURDAY(6, "星期六", "星期六感觉非常好"),
        SUNDAY(7, "星期日", "星期日感觉周末还没过够。。。");

        Day(int index, String name, String value) {
            this.index = index;
            this.name = name;
            this.value = value;
        }

        private int index;
        private String name;
        private String value;

        public int getIndex() {
            return index;
        }

        public void setIndex(int index) {
            this.index = index;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public String getValue() {
            return value;
        }

        public void setValue(String value) {
            this.value = value;
        }
    }

}
```

## 2. Main函数调用

```java
public class Main {

    public static void main(String[] args) {
	EnumTest2 firstDay = new EnumTest2(EnumTest2.Day.SUNDAY);
    firstDay.tellItLikeItIs();

    EnumTest2 thirdDay = new EnumTest2(EnumTest2.Day.WEDNESDAY);
    thirdDay.tellItLikeItIs();

    EnumTest2 fifthDay = new EnumTest2(EnumTest2.Day.FRIDAY);
    fifthDay.tellItLikeItIs();

    EnumTest2 sixthDay = new EnumTest2(EnumTest2.Day.SATURDAY);
    sixthDay.tellItLikeItIs();

    EnumTest2 seventhDay = new EnumTest2(EnumTest2.Day.SUNDAY);
    seventhDay.tellItLikeItIs();
    }
}
```

# 三. enum类内部定义方法

## 1.enum定义

```java
package com.company;

public class EnumTest3 {
    Day day;

    public EnumTest3(Day day) {
        this.day = day;
    }

    public void tellItLikeItIs() {
        switch (day) {
            case MONDAY:
                System.out.println(day.getName()+day.getValue());
                System.out.println(day.getName()+"的下一天是"+day.getNext().getName());
                break;

            case FRIDAY:
                System.out.println(day.getName()+day.getValue());
                System.out.println(day.getName()+"的下一天是"+day.getNext().getName());
                break;

            case SATURDAY: case SUNDAY:
                System.out.println(day.getName()+day.getValue());
                System.out.println(day.getName()+"的下一天是"+day.getNext().getName());
                break;

            default:
                System.out.println(day.getName()+day.getValue());
                System.out.println(day.getName()+"的下一天是"+day.getNext().getName());
                break;
        }
    }

    public enum Day {
        MONDAY(1, "星期一", "各种不在状态"){
            @Override
            public Day getNext() {
                return TUESDAY;
            }
        },
        TUESDAY(2, "星期二", "依旧犯困"){
            @Override
            public Day getNext() {
                return WEDNESDAY;
            }
        },
        WEDNESDAY(3, "星期三", "感觉半周终于过去了"){
            @Override
            public Day getNext() {
                return THURSDAY;
            }
        },
        THURSDAY(4, "星期四", "期待这星期五"){
            @Override
            public Day getNext() {
                return FRIDAY;
            }
        },
        FRIDAY(5, "星期五", "感觉还不错"){
            @Override
            public Day getNext() {
                return SATURDAY;
            }
        },
        SATURDAY(6, "星期六", "感觉非常好"){
            @Override
            public Day getNext() {
                return SUNDAY;
            }
        },
        SUNDAY(7, "星期日", "感觉周末还没过够。。。"){
            @Override
            public Day getNext() {
                return MONDAY;
            }
        };

        Day(int index, String name, String value) {
            this.index = index;
            this.name = name;
            this.value = value;
        }

        private int index;
        private String name;
        private String value;
        public abstract Day getNext();

        public int getIndex() {
            return index;
        }

        public void setIndex(int index) {
            this.index = index;
        }

        public String getName() {
            return name;
        }

        public void setName(String name) {
            this.name = name;
        }

        public String getValue() {
            return value;
        }

        public void setValue(String value) {
            this.value = value;
        }

    }
}
```



## 2. Main函数调用

```java
public class Main {

    public static void main(String[] args) {

    EnumTest3 firstDay = new EnumTest3(EnumTest3.Day.SUNDAY);
    firstDay.tellItLikeItIs();

    EnumTest3 thirdDay = new EnumTest3(EnumTest3.Day.WEDNESDAY);
    thirdDay.tellItLikeItIs();

    EnumTest3 fifthDay = new EnumTest3(EnumTest3.Day.FRIDAY);
    fifthDay.tellItLikeItIs();

    EnumTest3 sixthDay = new EnumTest3(EnumTest3.Day.SATURDAY);
    sixthDay.tellItLikeItIs();

    EnumTest3 seventhDay = new EnumTest3(EnumTest3.Day.SUNDAY);
    seventhDay.tellItLikeItIs();

    }
}
```

