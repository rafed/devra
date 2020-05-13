---
title: Parsing C++/Java/C# the Easy Way (with srcML)
date: 2019-11-19
lastmod: 2020-05-12
tags: [software engineering]
image: "image/srcml.png"
---

Recently I needed to parse C++ code to analyze some projects. I tried out several parsers (clang, libclang, cppast) but I just couldn't get them to work for me. I didn't find their documentation easy to understand. That's maybe because I'm not so familiar with the C++ ecosystem. I suffered for quite a while until I found this awesome tool called [srcML](https://www.srcml.org/).

srcML is a lightweight tool for the exploration of source code that presents source code in an XML format. Here's how it works. Suppose you have the following source code.

{{<highlight cpp>}}
#include<iostream>

using namespace std;

int main(){
    int a = 1;
    int b = 2;
    int c = a + b;
    
    cout << "The number is: " << c << endl;
}
{{</highlight>}}

To turn this into XML, download the tool and run

{{<highlight bash>}}
$ srcml file.cpp  
{{</highlight>}}

And you'll get this as output.

{{<highlight xml>}}
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<unit xmlns="http://www.srcML.org/srcML/src" xmlns:cpp="http://www.srcML.org/srcML/cpp" revision="0.9.5" language="C++" filename="sample.cpp"><cpp:include>#<cpp:directive>include</cpp:directive><cpp:file>&lt;iostream&gt;</cpp:file></cpp:include>

<using>using <namespace>namespace <name>std</name>;</namespace></using>

<function><type><name>int</name></type> <name>main</name><parameter_list>()</parameter_list><block>{
    <decl_stmt><decl><type><name>int</name></type> <name>a</name> <init>= <expr><literal type="number">1</literal></expr></init></decl>;</decl_stmt>
    <decl_stmt><decl><type><name>int</name></type> <name>b</name> <init>= <expr><literal type="number">2</literal></expr></init></decl>;</decl_stmt>
    <decl_stmt><decl><type><name>int</name></type> <name>c</name> <init>= <expr><name>a</name> <operator>+</operator> <name>b</name></expr></init></decl>;</decl_stmt>
    
    <expr_stmt><expr><name>cout</name> <operator>&lt;&lt;</operator> <literal type="string">"The number is: "</literal> <operator>&lt;&lt;</operator> <name>c</name> <operator>&lt;&lt;</operator> <name>endl</name></expr>;</expr_stmt>
}</block></function></unit>
{{</highlight>}}

After XML generation, it is rather easy to parse the code. There are plenty of neat XML parsing libraries out there. The XML element names are beautifully documented on their [site](https://www.srcml.org/documentation.html), so you shouldn't have a problem understanding the tags and parsing them. An advantage of using this tool is you can easily generate XML for other languages (although the supported languages are few). So you don't need to install and use different parsers for different languages. 

Although I was looking for an AST (abstract syntax tree) parser and though srcML does not generate AST, it still gave me sufficient XML data to work with. It's also very easy to use and works on all major platforms (Linux, Windows, macOS).

## Issues with srcML

On ubuntu, the following problem might occur.

{{<highlight bash>}}
srcml: /usr/lib/x86_64-linux-gnu/libcurl.so.4: version `CURL_OPENSSL_3' not found (required by srcml)  
{{</highlight>}}

To fix this, run

{{<highlight bash>}}
$ apt install libcurl3 libcurl-openssl1.0-dev  
{{</highlight>}}

~~Also, the project is somewhat old and doesn't seem like it is maintained. It is however open sourced at Github. Any open source contributors out there?~~ The authors of srcML received an award in MSR2020 for their contributions in software engineering. MSR is the leading software engineering conference in mining data from source code. So this project is very much alive!
