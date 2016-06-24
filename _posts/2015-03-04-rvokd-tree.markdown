---
author: mageric
comments: true
date: 2015-03-04 16:43:50+00:00
layout: post
title: RVO的kd-Tree
categories:
- 路径规划
tags:
- RVO
---
以下是RVO种的KD-Tree代码:    
{% highlight c++ %}
//kdTree.h
namespace RVO {
  class KdTree {
    private:  
       class AgentTreeNode {
          public:
           size_t begin;
           size_t end;
           size_t left;
           float maxX;
           float maxY;
           float minX;
           float minY;
           size_t right;
        };
    class ObstacleTreeNode {
     public:
     ObstacleTreeNode *left;
     const Obstacle *obstacle;
     ObstacleTreeNode *right;
    };
    //显式调用,无法隐式调用KdTree
    explicit KdTree(RVOSimulator *sim);
    ~KdTree();
    void buildAgentTree();
    void buildAgentTreeRecursive(size_t begin, size_t end, size_t node);
    void buildObstacleTree();
    ObstacleTreeNode *buildObstacleTreeRecursive(const std::vector<Obstacle *> &obstacles);
    void computeAgentNeighbors(Agent *agent, float &rangeSq) const;
    void computeObstacleNeighbors(Agent *agent, float rangeSq) const;
    void deleteObstacleTree(ObstacleTreeNode *node);
    void queryAgentTreeRecursive(Agent *agent, float &rangeSq,
    size_t node) const;
    void queryObstacleTreeRecursive(Agent *agent, float rangeSq,
    const ObstacleTreeNode *node) const;
    bool queryVisibility(const Vector2 &q1, const Vector2 &q2,
    float radius) const;
    bool queryVisibilityRecursive(const Vector2 &q1, const Vector2 &q2,float radius,
      const ObstacleTreeNode *node) const;
    std::vector<Agent *> agents_;
    std::vector<AgentTreeNode> agentTree_;
    ObstacleTreeNode *obstacleTree_;
    RVOSimulator *sim_;
    static const size_t MAX_LEAF_SIZE = 10;
    friend class Agent;
    friend class RVOSimulator;
    };
}
{% endhighlight %}

`AgentTreeNode`代表在场景中个体的节点结构，包括最大最小的二维空间数值、左侧右侧、开始与末尾节点的个数。
`ObstacleTreeBode`定义了障碍物的K-D树结构，包括左右子树、障碍数量属性。构造方法KdTree，仅支持显式调用。    
`buildAgentTree()` 构造个体kd树。   
`buildAgentTreeRecursive` 个体树递归。    
`buildObstacleTree()`构造障碍物树。    
`buildObstacleTreeRecursive()`递归调用构造 。    
`computeAgentNeighbors()`计算指定个体的邻居。     
`computeObstacleNeighbors()`计算指定个体的障碍物邻居。    
`deleteObstacleTree()`删除障碍物树。    
`queryAgentTreeRecursive()`  `queryObstacleTreeRecursive()` 查询函数。     
`queryVisibility()`  `queryVisibilityRecursive()`查询在指定范围内的两点间的可见性。如果在范围内可见，则范围true,否则false。   

 Obstacle结构：   
{% highlight c++ %}
    //Obstacle.h
  namespace RVO {
    /**
    * brief Defines static obstacles in the simulation.
    */
    class Obstacle {
    private:
    /*
    * brief Constructs a static obstacle instance.
    */
    Obstacle();
    bool isConvex_;
    Obstacle *nextObstacle_;
    Vector2 point_;
    Obstacle *prevObstacle_;
    Vector2 unitDir_;
    size_t id_;
    friend class Agent;
    friend class KdTree;
    friend class RVOSimulator;
    };
  }
{% endhighlight %}

总之先复制粘贴吧，以后慢慢改进~~
