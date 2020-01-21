**Mockery Vs Gomock**

Two of the most popular mock frameworks present in golang are [mockery](https://github.com/vektra/mockery) and [gomock](https://github.com/golang/mock/blob/master/README.md)


Both the frameworks are widely popular. Here are some key points that could help you decide which one to choose:

[Mockery](https://godoc.org/github.com/vektra/mockery/mockery):
1. Mockery provides you a very simple mocking framework that let's you dictate the input and expected output:
eg: 
```
mockSample.On("Insert", mockThing).Return(5)
```


[Gomock](https://godoc.org/github.com/golang/mock/gomock):

This is a nice article that helped me increase my understanding for gomock: https://blog.codecentric.de/en/2017/08/gomock-tutorial/

1. gomock provides functionality to pass **Times** parameter, which allows you to specify the number of times the function under consideration should run while executing some test.
This is a very handy feature and increases the quality of you test several times. 

eg: quoting the [article](https://blog.codecentric.de/en/2017/08/gomock-tutorial/):
```
mockDoer.EXPECT().DoSomething(123, "Hello GoMock").Return(nil).Times(1)
```
2. Another useful thing is ability to assert the call order:

eg: quoting the [article](https://blog.codecentric.de/en/2017/08/gomock-tutorial/):
```
callFirst := mockDoer.EXPECT().DoSomething(1, "first this")
callA := mockDoer.EXPECT().DoSomething(2, "then this").After(callFirst)
callB := mockDoer.EXPECT().DoSomething(2, "or this").After(callFirst)
```

or 
```
gomock.InOrder(
    mockDoer.EXPECT().DoSomething(1, "first this"),
    mockDoer.EXPECT().DoSomething(2, "then this"),
    mockDoer.EXPECT().DoSomething(3, "then this"),
    mockDoer.EXPECT().DoSomething(4, "finally this"),
)
```
3. Other features include the argument matchers, the ability to specifying mock actions.


Based on the features we discussed, gomock is the winner. Go for gomock if you are still confused what to choose :+1:
