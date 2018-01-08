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

GTest有两个版本的断言宏，`ASSERT_*`和`EXPECT_*`。`ASSERT_*`类断言宏失败时会终止当前被测程序，而`EXPECT_*`类断言宏则不会。

自定义的失败消息可以使用`<<`运算符传递给断言宏。断言失败时，将打印参数和自定义的消息。如果参数支持`<<`运算符，将会调用它来打印参数。

| Fatal assertion | Nonfatal assertion | Verifies |
|---|---|---|
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

## Google Mock