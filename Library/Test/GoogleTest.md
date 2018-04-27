## Google Test

### Note

* __test case name__ 和 __test name__不应包含下划线`_`。

### Simple Test

``` C++
TEST(test_case_name, test_name) {
	//  test body
}
```

在Google Test执行时，首先将按照注册顺序，依次调用`Environment::SetUp()`函数。随后，Google Test将执行全部测试，

``` C++
class Environment : public ::testing::Environment {
public:
	virtual ~Environment() {}
	// Override this to define how to set up the environment.
	virtual void SetUp() {}
	// Override this to define how to tear down the environment.
	virtual void TearDown() {}
};

class Fixture : public ::testing::Test {
	//  You can remove any or all of the following functions if its body is empty.
protected:
	// Per-test-case set-up.
	// Called before the first test in this test case.
	// Can be omitted if not needed.
	static void SetUpTestCase() {
		shared_resource_ = new ...;
	}

	// Per-test-case tear-down.
	// Called after the last test in this test case.
	// Can be omitted if not needed.
	static void TearDownTestCase() {
		delete shared_resource_;
		shared_resource_ = NULL;
	}

	// Some expensive resource shared by all tests.
	static T* shared_resource_;
	
protected:
	Fixture() {
		//  You can do set-up work for each test here.
	}

	virtual ~Fixture() {
		//  You can do clean-up work that doesn't throw exceptions here.
	}

	//  If the constructor and destructor are not enough for setting up
	//  and cleaning up each test, you can define the following methods:

	virtual void SetUp() {
		//  Code here will be called immediately after the constructor (right before each test).
	}

	virtual void TearDown() {
		//  Code here will be called immediately after each test (right before the destructor).
	}

	// Objects declared here can be used by all tests in the test case for Foo.
};

TEST_F(Fixture, Test) {
	//  test body
}

int main(int argc, char **argv) {
	::testing::InitGoogleTest(&argc, argv);
	::testing::AddGlobalTestEnvironment(Environment);
	return RUN_ALL_TESTS();
}
```

### Assertion

__Google Test__ 有两个版本的断言宏，`ASSERT_*`和`EXPECT_*`。`ASSERT_*`类断言宏失败时会终止当前被测程序，而`EXPECT_*`类断言宏则不会。`ASSERT_*`类断言宏只能在返回值为`void`的函数中使用。

自定义的失败消息可以使用`<<`运算符传递给断言宏。断言失败时，将打印参数和自定义的消息。如果参数支持`<<`运算符，将会调用它来打印参数。

| Fatal assertion | Nonfatal assertion | Verifies |
|---|---|---|
| `SUCCEED();` |  | generate a success |
| `FAIL();` |  | generate a fatal failure |
|  | `ADD_FAILUER();` | generate a nonfatal failure |
|  | `ADD_FAILUER_AT("file_path", line_number);` | generate a nonfatal failure |
| `ASSERT_TRUE(condition);` | `EXPECT_TRUE(condition);` | `condition` is true |
| `ASSERT_FALSE(condition);`| `EXPECT_FALSE(condition);` | `condition` is false |
| `ASSERT_EQ(val1, val2);`|`EXPECT_EQ(val1, val2);`| `val1 == val2` is true |
| `ASSERT_NE(val1, val2);`|`EXPECT_NE(val1, val2);`| `val1 != val2` is true |
| `ASSERT_LT(val1, val2);`|`EXPECT_LT(val1, val2);`| `val1 < val2` is true |
| `ASSERT_LE(val1, val2);`|`EXPECT_LE(val1, val2);`| `val1 <= val2` is true |
| `ASSERT_GT(val1, val2);`|`EXPECT_GT(val1, val2);`| `val1 > val2` is true |
| `ASSERT_GE(val1, val2);`|`EXPECT_GE(val1, val2);`| `val1 >= val2` is true |
| `ASSERT_STREQ(str1, str2);` | `EXPECT_STREQ(str1, str2);` | the two C strings have the same content |
| `ASSERT_STRNE(str1, str2);` | `EXPECT_STRNE(str1, str2);` | the two C strings have different content |
| `ASSERT_STRCASEEQ(str1, str2);`| `EXPECT_STRCASEEQ(str1, str2);` | the two C strings have the same content, ignoring case |
| `ASSERT_STRCASENE(str1, str2);`| `EXPECT_STRCASENE(str1, str2);` | the two C strings have different content, ignoring case |
| `ASSERT_THROW(statement, exception_type);` | `EXPECT_THROW(statement, exception_type);` | statement throws an exception of the given type |
| `ASSERT_ANY_THROW(statement);` | `EXPECT_ANY_THROW(statement);` | statement throws an exception of any type |
| `ASSERT_NO_THROW(statement);` | `EXPECT_NO_THROW(statement);` | statement doesn't throw any exception |
| `ASSERT_PRED1(pred1, val1);` | `EXPECT_PRED1(pred1, val1);` | `pred1(val1)` returns true |
| `ASSERT_PRED2(pred2, val1, val2);` | `EXPECT_PRED2(pred2, val1, val2);` | `pred2(val1, val2)` returns true |
| `ASSERT_PRED3(pred5, val1, val2, val3);` | `EXPECT_PRED3(pred5, val1, val2, val3);` | `pred3(val1, val2, val3)` returns true |
| `ASSERT_PRED4(pred5, val1, val2, val3, val4);` | `EXPECT_PRED4(pred5, val1, val2, val3, val4);` | `pred4(val1, val2, val3, val4)` returns true |
| `ASSERT_PRED5(pred5, val1, val2, val3, val4, val5);` | `EXPECT_PRED5(pred5, val1, val2, val3, val4, val5);` | `pred5(val1, val2, val3, val4, val5)` returns true |
| `ASSERT_PRED_FORMAT1(pred_format1, val1);` | `EXPECT_PRED_FORMAT1(pred_format1, val1);` | `pred_format1(val1)` is successful |
| `ASSERT_PRED_FORMAT2(pred_format2, val1, val2);` | `EXPECT_PRED_FORMAT2(pred_format2, val1, val2);` | `pred_format2(val1, val2)` is successful |
| `ASSERT_PRED_FORMAT3(pred_format1, val1, val2, val3);` | `EXPECT_PRED_FORMAT3(pred_format1, val1, val2, val3);` | `pred_format3(val1, val2, val3)` is successful |
| `ASSERT_PRED_FORMAT4(pred_format1, val1, val2, val3, val4);` | `EXPECT_PRED_FORMAT4(pred_format1, val1, val2, val3, val4);` | `pred_format4(val1, val2, val3, val4)` is successful |
| `ASSERT_PRED_FORMAT5(pred_format1, val1, val2, val3, val4, val5);` | `EXPECT_PRED_FORMAT5(pred_format1, val1, val2, val3, val4, val5);` | `pred_format5(val1, val2, val3, val4, val5)` is successful |
| `ASSERT_FLOAT_EQ(val1, val2);` | `EXPECT_FLOAT_EQ(val1, val2);` | the two float values are almost equal |
| `ASSERT_DOUBLE_EQ(val1, val2);` | `EXPECT_DOUBLE_EQ(val1, val2);` | the two double values are almost equal |
| `ASSERT_NEAR(val1, val2, abs_error);` | `EXPECT_NEAR(val1, val2, abs_error);` | the difference between `val1` and `val2` doesn't exceed the given absolute error |
| `ASSERT_NO_FATAL_FAILURE(statement);` | `EXPECT_NO_FATAL_FAILURE(statement);` | `statement` doesn't generate any new fatal failures in the current thread. |

### Test Fixture

__Test Fixture__ 可以让多个测试使用相同的配置而无须多次编写初始化函数。对于每个测试， __Test Fixture__ 都会实例化一个新的实例。

使用 __Test Fixture__ 首先从`::testing::Test`中派生一个类。在类的构造函数或者`SetUp()`函数中编写初始化代码，在析构函数或者`TearDown()`函数中编写释放代码。注意，优先使用构造函数和析构函数编写代码，除非析构时可能抛出异常，使用`--gtest_throw_on_failure`参数进行测试或者调用虚函数。最后，使用`TEST_F`宏编写测试。

### Logging Additional Information

``` C++
RecordProperty("key", value);
```

### Death Test

__Death Test__ 是检查被测单元是否按预期的方式终止的测试。

| Fatal assertion | Nonfatal assertion | Verifies |
|---|---|---|
| `ASSERT_DEATH(statement, regex);` | `EXPECT_DEATH(statement, regex);` | `statement` crashes with the given error |
| `ASSERT_DEATH_IF_SUPPORTED(statement, regex);` | `EXPECT_DEATH_IF_SUPPORTED(statement, regex);` | if death tests are supported, verifies that `statement` crashes with the given error; otherwise verifies nothing |
| `ASSERT_EXIT(statement, predicate, regex);` | `EXPECT_EXIT(statement, predicate, regex);` | `statement` exits with the given error and its exit code matches `predicate` |

### Parameterize Test

#### Value Parameterized Tests

__Value Parameterized Tests__ 允许测试代码使用多套不同的输入参数进行测试而无须重复编写测试代码。编写 __Value Parameterized Tests__ 测试首先需要定义一个从`::testing::Test`和`::testing::WithParamInterface<T>`继承的`fixture`类。然后，使用`TEST_P`宏定义测试，并在测试中调用`GetParam()`函数获取输入参数进行测试。最后，使用`INSTANTIATE_TEST_CASE_P(InstantiationName, TestName, ValueSet);`实例化多个测试。

#### Type Parameterized Tests

__Type Parameterized Tests__ 可以对不同类型的参数进行相同的逻辑测试而无须重复编写测试代码。编写 __Type Parameterized Tests__ 测试首先需要定义一个带参数模板并从`::testing::Test`继承的`fixture`模板类。然后使用`TYPED_TEST_CASE(FixtureName, TypeSet);`添加类型列表。最后使用`TYPED_TEST()`宏编写测试。

## Google Mock
