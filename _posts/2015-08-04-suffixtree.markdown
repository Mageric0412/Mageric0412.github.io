---
author: mageric
comments: true
date: 2015-08-04 10:44:24+00:00
layout: post
title: 后缀树样例
categories:
- 算法
tags:
- 字符串处理
---
&#160; &#160; &#160; &#160;查询串s中是否存在子串P，主要针对于多个子串在一个主串中的匹配问题。     
建立后缀树：
{% highlight c %}  
    class SuffixTreeNode{
       map<char,SuffixTreeNode*> childTrees;
       char value;
       vector posIndex;  
     public:
       SuffixTreeNode(){}    
       void InsertString(string s,int index){
          posIndex.push_back(index); //对插入的顶点在处理串中的位置进行记录
         if(s.length()==0){
         value=s[0];
         SuffixTreeNode* child=NULL;
          if(childTrees.find(value)!=childTrees.end())
           {
             child=childTrees[value];
           }
           else {
             child=new SuffixTreeNode();
             childTrees[value]=child;
             }
           string lastString=s.substr(1); //对除了首字符之外的子串继续处理
           child->InsertString(lastString,index); //递归插入子串
          }
       }  
        //获取满足匹配条件的字串在主串的位置
        vector getPosition(string s){
         if(s.length()==0)
             return posIndex;
         else{
           char first=s[0];
           if(childTrees.find(first)!=childTrees.end()){
               string lastString=s.substr(1);
               return childTrees[first]->getPosition(lastString); //递归调用函数，直到匹配处理完毕
              }else{
               vector noPos;
               return noPos;
              }
           }
        }//getposition end
       //析构
       ~SuffixTreeNode(){
           map<char,SuffixTreeNode*>:: iterator itr;
          for(itr=childTrees.begin();itr!=childTrees.end();itr++)
             delete(itr->second);
         }
     };  
    ​//后缀树
      class SuffixTree{
        SuffixTreeNode* root;
        public:
         SuffixTree(string s){
           root=new SuffixTreeNode();
           for(int i=0;i<s.length();i++) //构造根节点，对字串进行斩头处理，构造后缀树 ​ { ​ string suffix=s.substr(i); ​ root->InsertString(suffix,i);
    ​       }
        }    ​
         //调用节点的获取子串在主串的位置方法
    ​    vector getRootPos(string s) {
    ​       return root->getPosition(s);
        }    ​
    ​   ~SuffixTree(){
    ​      if(root!=NULL) delete root;
    ​    }  ​
     };
     ​//测试主函数
     ​void main(){
        string test​String="thisishello";
    ​    string stringList[]{"this","is","shell","she"};
    ​    SuffixTree DicSufTree(testString);
    ​     for(int i=0;i<4;i++){
    ​       vector pos=DicSufTree.getRootPos(stringList[i]);
    ​        if(pos.size()!=0){
    ​            cout<<stringList[i].c_str()<<" ";
    ​               for(int j=0; j<pos.size();j++)
    ​                     cout<<pos[j]<<" ";
    ​             cout<<endl;
    ​        }
        }
     ​};
{% endhighlight %}  
