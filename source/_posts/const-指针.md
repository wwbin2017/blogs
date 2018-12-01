---
title: const 指针
date: 2018-08-11 15:21:09
tags: C++
---
#### const 和 指针容易混淆的地方
```C++
int main()
{
        // 引用& 和常量修饰const
        int a = 0;
        const int &r1 = a; // const 只是限定r1不能修改，但是a本身是可以修改的
        a = 1;
        // int &r4 = 1;  #错误，右边得是对象


        //指针和const
        const double pi = 3.14;
        // double *ptr = &pi;   # 错误因为ptr是普通指针 \
                                其实就是两边类型不一致，double 和 const double
        const  double *cptr = &pi; // cptr并没有限定cptr是const，\
                                        cptr还是可以改变的。
        // 指针的类型必须与所指向的类型保持一致
        // 存在两个例外
        double dval = 3.14;
        cptr = &dval;   // 不能通过cptr改变值

        // const 指针
        int errNum = 0;
        int *const curErr = &errNum; //curErr是const，其值不允许修改，\
                                        即不能指向其他对象，但是可以改变对象的值

        *curErr = 10;
        const double* const pip = &pi;//pip的值不允许修改，同时也不允许通过*pip修改
        //*pip = 0.0;  错误


        return 0;
}
```
