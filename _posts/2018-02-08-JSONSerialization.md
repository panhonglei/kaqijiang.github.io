---
date: 2018-02-08 15:27:31
layout: post
title: JSONSerialization及参数详解
category: Swift
tags: Swift
keywords: JSONSerialization ReadingOptions mutableContainers mutableLeaves allowFragments WritingOptions prettyPrinted
description: JSONSerialization及参数详解
---


JSONSerialization及参数详解


### JSONSerialization文档中的解释


>  A class for converting JSON to Foundation objects and converting Foundation objects to JSON.
> 
>  An object that may be converted to JSON must have the following properties:
> 
> - Top level object is an NSArray or NSDictionary
> 
> - All objects are NSString, NSNumber, NSArray, NSDictionary, or NSNull
> 
> - All dictionary keys are NSStrings
> 
> - NSNumbers are not NaN or infinity


> > #### 将JSON转换为Foundation对象并将Foundation对象转换为JSON的类。
> >
> > #### 可以转换为JSON的对象必须具有以下属性：
> >
> >- 顶级对象是一个NSArray或NSDictionary
> >
> >- 所有对象都是NSString，NSNumber，NSArray，NSDictionary或NSNull
> >
> >- 所有字典键都是NSStrings
> >- NSNumbers不是NaN或无穷大



### JSONSerialization继承自NSObject,包含以下类方法


>  - #### open class func isValidJSONObject(_ obj: Any) -> Bool<br>
对象可以转换为JSON数据，则返回YES，否则返回NO

> - #### open class func data(withJSONObject obj: Any, options opt: JSONSerialization.WritingOptions = []) throws -> Data<br>
	- 从Foundation对象生成JSON数据。 如果对象不会生成有效的JSON，则会抛出异常。<br> 
	- 设置NSJSONWritingPrettyPrinted选项生成格式化的JSON，使输出更具可读性。<br> 
	- 如果没有设置该选项"[]"，则会生成最紧凑的JSON。 <br>
如果发生错误，错误参数将被设置，返回值将为零。 结果数据是用UTF-8编码的。

> - #### open class func jsonObject(with data: Data, options opt: JSONSerialization.ReadingOptions = []) throws -> Any<br>
	- 以JSON数据创建一个Foundation对象。

> - #### open class func writeJSONObject(_ obj: Any, to stream: OutputStream, options opt: JSONSerialization.WritingOptions = [], error: NSErrorPointer) -> Int<br>
	- 将JSON数据写入流中。 该流应该打开并配置。 
	- 返回值是写入流的字节数，或者是错误的0。 
	- 此方法的所有其他行为与dataWithJSONObject：options：error：method相同。

> - #### open class func jsonObject(with stream: InputStream, options opt: JSONSerialization.ReadingOptions = []) throws -> Any<br>
	- 从JSON数据流创建一个JSON对象。 该流应该打开并配置。 
	- 此方法的所有其他行为与JSONObjectWithData：options：error：方法相同。


### 参数


> #### ReadingOptions
- 从JSON数据创建Foundation对象时使用的选项

> #### mutableContainers
- 返回的数组和字典都是NSMutableArray和NSMutableDictionay类型，可以作后续修改,如果data数据既不是数组也不是字典，或者说格式错误，那么返回nil并抛出错误。

> #### mutableLeaves
- 表示如果data是字典或数组的前提下，将data转为可变字符串。

> #### allowFragments
- 需要格式化的json字符串最外层可以不是数组和字典，只要是正确的json格式就行。

-

> #### WritingOptions
- 写入JSON数据的选项。

> #### prettyPrinted
- 生成的json字符串是带换行和缩进的，更加易读。如果要生成单行不带缩进的就直接设0。

> #### sortedKeys ios11
- 使用[NSLocale systemLocale]对输出的字典键进行排序。 
- 键使用NSNumericSearch进行比较。 所使用的具体分类方法可能会发生变化。

#### 对象转换为JSON数据 prettyPrinted
```
let dict = [
			  "name":"zhangSan",
			  "age":18
			  ] as [String: Any]

		do {
            let jsonData = try JSONSerialization.data(withJSONObject: dict, options: .prettyPrinted)
            let ss = String(data: jsonData, encoding: .utf8)
            print(ss ?? "")
        } catch  {
            print("error")
        }
//options可传入[] {"name":"zhangSan","age":18}
//prettyPrinted 显示换行
//	{
// "name" : "zhangSan",
//  "age" : 18
//	}
```

#### JSON数据转对象 mutableContainers可变数组或字典
```
do {
            
            guard let jsonObject = jsonStr?.data(using: .utf8) else {
                print("error")
                return
            }
            var dict = try JSONSerialization.jsonObject(with: jsonObject, options: .mutableContainers) as! [String: Any]
            print(dict)
        } catch  {
            print("error")
            return
        }
        //["name": zhangSan, "age": 18]
```
#### JSON数据转对象 allowFragments可变数组或字典
```
do {
           let jsonStr = "344"
            
            guard let jsonObject = jsonStr?.data(using: .utf8) else {
                print("error")
                return
            }
            var dict = try JSONSerialization.jsonObject(with: jsonObject, options: . allowFragments) as! [String: Any]
            print(dict)
        } catch  {
            print("error")
            return
        }
        //344
```

#### JSON数据转对象 mutableLeaves 数据是字典或数组的前提下，将数据转为可变字符串。
```
do {
           let jsonStr = "[23]"
            
            guard let jsonObject = jsonStr?.data(using: .utf8) else {
                print("error")
                return
            }
            var dict = try JSONSerialization.jsonObject(with: jsonObject, options: . mutableLeaves) as! [String: Any]
            print(dict)
        } catch  {
            print("error")
            return
        }
        //(23)
```

### 特殊情况处理：
在和JS后台交换数据时，会出现这么种情况：字典的关键不是字符串类型的要知道JS的JSON允许这么做，但是IOS的JSONSerialization是不允许的于是会出现这么种数据。
>  一个JSON字符串，遵循格式{ name: "John" }而不是{ "name" : "John"}

这个数据我们解析的时候回抛出异常，因为这顶层是{}包围的字典格式，但是内部却不是我们要求的Key是字符串。

```
import WebKit
class MyJSONParser {
    private static let webView = WKWebView()

    class func parse(jsonString: String, completionHandler: @escaping (Any?, Error?) -> Void) {
        self.webView.evaluateJavaScript(jsonString, completionHandler: completionHandler)
    }
}

let str = "{ firstName: 'John', lastName: 'Smith' }"

// You must assign the JSON string to a variable or the Javascript
// will return void. Note that this runs asynchronously
MyJSONParser.parse(jsonString: "tmp = \(str)") { result, error in
    guard error == nil else {
        print(error!)
        return
    }
    if let dict = result as? [String: String] {
        print(dict)
    } else {
        print("Can't convert to Dictionary")
    }
}
```