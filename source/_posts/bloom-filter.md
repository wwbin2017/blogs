---
title: bloom filter
date: 2018-07-14 20:38:44
tags: 数据结构及算法
---

### bitmap
bitmap位图可以认为是把一个数映射到一个空间，最常用的就是hash但是hash在数据量大的时候就不管用了或者效率不高了。因此我们可以用位图来给元素做一一映射，一个数据如果在bitmap中其对应的位置为1否则为0。我们做一个简单的统计，计算int为32个bit，因此总共有2^32个数，因此我们需要相当的bit来做一个一一映射。因此需要的空间大小为2^32/(8*1024*2024)=2^32/2^23=2^9=512M.

```c++
#include<iostream>
#include<vector>
using namespace std;
class BitMap
{
private:
    vector<size_t> array;
public:
    BitMap(){}
    BitMap(size_t num)
    {
        set_cloumn(num);
    }
    void set_cloumn(size_t num)
    {
        // 一个size_t存32个数,32位
        array.resize((num>>5)+1);
    }
    size_t calc_index(size_t num)
    {
        return num>>5;
    }
    size_t calc_pos(size_t num)
    {
        return num%32;
    }
    bool add(size_t num)
    {
        size_t pos = calc_pos(num);
        size_t index = calc_index(num);
        if(index>=array.size())
            return false;
        array[index] |= (0x01<<pos);
        return true;
    }
    bool clear(size_t num)
    {
        size_t pos = calc_pos(num);
        size_t index = calc_index(num);
        if(index>=array.size())
            return false;
        array[index] &= ~(0x01<<pos);
    }
    bool is_contains(size_t num)
    {
        size_t pos = calc_pos(num);
        size_t index = calc_index(num);
        if(index>=array.size())
            return false;
        if(array[index]&(0x01<<pos))
                return true;
        return false;
    }
};
```
### BitMap评价
* 可以对空间进行压缩
* 快速排序，去重，查询（类似hash，其实就是一个hash，一一映射）
* 运算效率高 不做比较，基本上是位运算
* 当然以上优点是针对数据比较密集的时候，否则还是有很大浪费的
***
### Boom filter
Bloom Fliter是Bit-map思想的一种扩展，基本做法就是使用k个hash函数，分别映射到固定范围，因此一个数据会使得k个位置为1,判断元素是否在集合中，是k个位置都为1。因此我们可以知道会存在误判的情况。允许低错误率的场景下，大大地进行空间压缩，是一种拿错误率换取空间的数据结构。
```c++
class Bloom_Filter
{
public:
        Bloom_Filter(size_t size)
                :_capacity(size)
        {
                _bitmap.set_cloumn(size);
        }

        void add(const K& key)
        {
                _bitmap.add(HashFun1()(key) % _capacity);
                _bitmap.add(HashFun2()(key) % _capacity);
                _bitmap.add(HashFun3()(key) % _capacity);
                _bitmap.add(HashFun4()(key) % _capacity);
                _bitmap.add(HashFun5()(key) % _capacity);
        }

        bool is_contains(const K& key)
        {
                if (!_bitmap.is_contains(HashFun1()(key) % _capacity))
                        return false;
                if (!_bitmap.is_contains(HashFun2()(key) % _capacity))
                        return false;
                if (!_bitmap.is_contains(HashFun3()(key) % _capacity))
                        return false;
                if (!_bitmap.is_contains(HashFun4()(key) % _capacity))
                        return false;
                if (!_bitmap.is_contains(HashFun5()(key) % _capacity))
                        return false;
                return true;
        }
private:
        BitMap _bitmap;
        size_t _capacity;
};
```
