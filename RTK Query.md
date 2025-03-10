## RTK Query

### 创建API切片

RTKQ中将一组相关功能统一封装到一个Api对象中：

```react
import {createApi, fetchBaseQuery} from "@reduxjs/toolkit/dist/query/react";

export const studentApi = createApi({
    reducerPath:'studentApi',
    baseQuery:fetchBaseQuery({
        baseUrl:'http://localhost:9999/'
    }),
    endpoints(build) {
        return {
            getStudents: build.query({
                query() {
                    return 'data'
                }
            }),
        }
    }
});

export const {useGetStudentsQuery} = studentApi;
```

+ reducerPath：用来设置reducer的唯一标识，主要用来在创建store时指定action的type属性，如果不指定默认为api。
+ baseQuery：用来设置发送请求的工具，就是你是用什么发请求，RTKQ为我们提供了fetchBaseQuery作为查询工具，它对fetch进行了简单的封装。
+ fetchBaseQuery：简单封装过的fetch调用后会返回一个封装后的工具函数。需要一个配置对象作为参数，baseUrl表示Api请求的基本路径，指定后请求将会以该路径为基本路径。
+ endpoints：与服务器交互而定义的一组操作，请求接口可以是 `queries`，它返回用于缓存的数据，或者是`mutations`，它向服务器发送更新。 请求接口是使用回调函数定义的，该函数接受 `builder` 参数并返回一个对象，该对象包含使用 `builder.query()` 和 `builder.mutation()` 创建的请求接口定义。
+ 上述代码中的`useGetStudentsQuery`是自动定义的hook， 封装了在组件挂载时触发请求的过程，以及在处理请求和数据可用时重新渲染组件的过程。

### 创建store对象

```react
import {configureStore} from "@reduxjs/toolkit";
import {studentApi} from "./studentApi";

export const store = configureStore({
    reducer:{
        [studentApi.reducerPath]:studentApi.reducer
    },
    middleware:getDefaultMiddleware =>
        getDefaultMiddleware().concat(studentApi.middleware),
});
```

+ API slice 会生成需要添加到 store 的自定义 middleware。这个 middleware *必须* 被添加——它管理缓存的生命周期和控制是否过期。

```react
import React from 'react';
import {useGetStudentsQuery} from './store/studentApi';

const App = () => {
    const {data, isFetching, isSuccess} = useGetStudentsQuery();

    return (
        <div>
            {isFetching && <p>数据正在加载...</p>}
            {isSuccess && data.data.map(item => <p key={item.id}>
                {item.attributes.name} --
                {item.attributes.age} --
                {item.attributes.gender} --
                {item.attributes.address}
            </p>)}
        </div>
    );
};

export default App;
```

直接调用`useGetStudentsQuery()`它会自动向服务器发送请求加载数据，并返回一个对象。：

+ data – 最新返回的数据。
+ currentData – 当前的数据
+ error – 错误信息
+ isUninitialized – 如果为true则表示查询还没开始
+ isLoading – 为true时，表示请求正在第一次加载
+ isFetching 为true时，表示请求正在加载
+ isSuccess 为true时，表示请求发送成功
+ isError 为true时，表示请求有错误
+ refetch 函数，用来重新加载数据。