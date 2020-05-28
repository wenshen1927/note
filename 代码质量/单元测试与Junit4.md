# 单元测试与Junit4

## 为什么单元测试

- 天然的方法说明文档
- 代码质量的保证
- 持续重构的定心丸

## 测试什么

- 某个模块(如Service层的方法)，公共的API，不要对private方法单元测试
- 常用的输入输出组合
- 边界条件和异常

## Junit

### 常用注解

| 注解                              | 说明                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| @BeforeClass                      | 在所有测试方法执行前执行一次，一般在其中写上整体初始化的代码，要求方法static |
| @AfterClass                       | 在所有测试方法后执行一次，一般在其中写上销毁和释放资源的代码，要求方法static |
| @Before                           | 在每个@Test注解的方法执行之前执行                            |
| @After                            | 在每个@Test注解的方法执行之后执行                            |
| @Test                             | 测试方法，一般的测试用例                                     |
| @Test(timeout = 1000)             | 测试方法执行超过1000毫秒后算超时，测试将失败                 |
| @Test(expected = Exception.class) | 测试方法期望得到的异常类，如果方法执行没有抛出指定的异常，则测试失败 |
| @Ignore("not ready yet")          | 执行测试时将忽略掉此方法，如果用于修饰类，则忽略整个类       |

详细注解：<https://junit.org/junit5/docs/current/user-guide/>

#### 无依赖的单元测试

@Test

### Mockito

| 注解      | 说明                       |
| --------- | -------------------------- |
| @SpyBean  | mock一个对象，解决依赖问题 |
| @MockBean | 只mock部分方法             |
|           |                            |

有依赖的单元测试

@MockBean

A->B



@SpyBean

A->B的某一个方法



手动获取Mock对象



Mockito.mock(B.class,,Mockito.RETURNS_DEEP_STUBS)

A->B->C的某一个方法

### 数据打桩



## 个人理解

- UT代码要简单
- 善用Mock和Spy
- UT并不能保证完全没bug

## 参考

<https://www.jianshu.com/p/ecbd7b5a2021>