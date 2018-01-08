## Google Test

### Simple Test

``` C++
TEST(test_case_name, test_name) {
    //  test body
}
```

``` C++
class FixtureTest : public ::testing::Test {
protected:
    //  You can remove any or all of the following functions if its body is empty.

    FixtureTest() {
        //  You can do set-up work for each test here.
    }

    virtual ~FixtureTest() {
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

TEST_F(FixtureTest, test_name) {
  //  test body
}

int main(int argc, char **argv) {
  ::testing::InitGoogleTest(&argc, argv);
  return RUN_ALL_TESTS();
}
```

### Assertion

GTest有两个版本的断言宏，`ASSERT_*`和`EXPECT_*`。`ASSERT_*`类断言宏失败时会终止当前被测程序，而`EXPECT_*`类断言宏则不会。`ASSERT_*`类断言宏只能在返回值为`void`的函数中使用。

自定义的失败消息可以使用`<<`运算符传递给断言宏。断言失败时，将打印参数和自定义的消息。如果参数支持`<<`运算符，将会调用它来打印参数。

| Fatal assertion | Nonfatal assertion | Verifies |
|---|---|---|
| `SUCCEED();` |  | generate a success |
| `FAIL();` |  | generate a fatal failure |
| `ADD_FAILUER();` |  | generate a nonfatal failure |
| `ADD_FAILUER_AT("file_path", line_number);` |  | generate a nonfatal failure |
| `ASSERT_TRUE(condition);` | `EXPECT_TRUE(condition);` | `condition` is true |
| `ASSERT_FALSE(condition);`| `EXPECT_FALSE(condition);` | `condition` is false |
| `ASSERT_EQ(val1, val2);`|`EXPECT_EQ(val1, val2);`| `val1 == val2` |
| `ASSERT_NE(val1, val2);`|`EXPECT_NE(val1, val2);`| `val1 != val2` |
| `ASSERT_LT(val1, val2);`|`EXPECT_LT(val1, val2);`| `val1 < val2` |
| `ASSERT_LE(val1, val2);`|`EXPECT_LE(val1, val2);`| `val1 <= val2` |
| `ASSERT_GT(val1, val2);`|`EXPECT_GT(val1, val2);`| `val1 > val2` |
| `ASSERT_GE(val1, val2);`|`EXPECT_GE(val1, val2);`| `val1 >= val2` |
| `ASSERT_STREQ(str1, str2);` | `EXPECT_STREQ(str1, str2);` | the two C strings have the same content |
| `ASSERT_STRNE(str1, str2);` | `EXPECT_STRNE(str1, str2);` | the two C strings have different content |
| `ASSERT_STRCASEEQ(str1, str2);`| `EXPECT_STRCASEEQ(str1, str2);` | the two C strings have the same content, ignoring case |
| `ASSERT_STRCASENE(str1, str2);`| `EXPECT_STRCASENE(str1, str2);` | the two C strings have different content, ignoring case |
| `ASSERT_THROW(`_statement_, _exception\_type_`);`  | `EXPECT_THROW(`_statement_, _exception\_type_`);`  | _statement_ throws an exception of the given type  |
| `ASSERT_ANY_THROW(`_statement_`);`                | `EXPECT_ANY_THROW(`_statement_`);`                | _statement_ throws an exception of any type        |
| `ASSERT_NO_THROW(`_statement_`);`                 | `EXPECT_NO_THROW(`_statement_`);`                 | _statement_ doesn't throw any exception            |
| `ASSERT_PRED1(`_pred1, val1_`);`       | `EXPECT_PRED1(`_pred1, val1_`);` | _pred1(val1)_ returns true |
| `ASSERT_PRED2(`_pred2, val1, val2_`);` | `EXPECT_PRED2(`_pred2, val1, val2_`);` |  _pred2(val1, val2)_ returns true |
|  ...                | ...                    | ...          |
| `ASSERT_PRED5(`_pred5, val1_`);`       | `EXPECT_PRED5(`_pred1, val1_`);` | _pred5(val1)_ returns true |
| `ASSERT_PRED_FORMAT1(`_pred\_format1, val1_`);`        | `EXPECT_PRED_FORMAT1(`_pred\_format1, val1_`);` | _pred\_format1(val1)_ is successful |
| `ASSERT_PRED_FORMAT2(`_pred\_format2, val1, val2_`);` | `EXPECT_PRED_FORMAT2(`_pred\_format2, val1, val2_`);` | _pred\_format2(val1, val2)_ is successful |
| `...`               | `...`                  | `...`        |
| `ASSERT_PRED_FORMAT5(`_pred\_format1, val1_`);`        | `EXPECT_PRED_FORMAT5(`_pred\_format1, val1_`);` | _pred\_format1(val1)_ is successful |
| `ASSERT_FLOAT_EQ(`_val1, val2_`);`  | `EXPECT_FLOAT_EQ(`_val1, val2_`);` | the two `float` values are almost equal |
| `ASSERT_DOUBLE_EQ(`_val1, val2_`);` | `EXPECT_DOUBLE_EQ(`_val1, val2_`);` | the two `double` values are almost equal |
| `ASSERT_NEAR(`_val1, val2, abs\_error_`);` | `EXPECT_NEAR`_(val1, val2, abs\_error_`);` | the difference between _val1_ and _val2_ doesn't exceed the given absolute error |

## Google Mock