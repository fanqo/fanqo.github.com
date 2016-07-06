---
layout: post
title: "使用Paraview查看OpenFOAM中blockMeshDict的节点编号"
description: ""
category: OpenFOAM
tags: [ParaView, OpenFOAM, blockMesh, objToVTK]
---
{% include JB/setup %}
用 VirtualBox 装了个 Archlinux ，然后在里面编译了 OpenFOAM 3.0.1和4.0来进行 OpenFOAM 的学习。为了保持虚拟机较小，就没有安装图形界面，而是通过 putty ssh 登录到 guest OS (Archlinux) 上来执行 OpenFOAM ，将运算完成的数据通过 WinSCP 取下来在 host OS (Windows 7) 上进行处理。此为背景。
今天练习 damBreak 这个实例，看到 blockMeshDict 中有个 atmosphere boundary ，该 boundary 由三个面组成，一时想不出来是哪三个面，就想着是否有办法查看一下该 blockMeshDict 中指定的节点编号，从而再来确定是由哪三个面组成的 atmosphere 。放 Google 搜了一下，好像 `paraFoam -block` 就可以用来显示节点的编号。因为我虚拟机中就没有安装图形界面，也就没安装ParaView，所以也就无从执行该命令。然后就发现了[这里](http://www.cfd-online.com/Forums/openfoam-meshing-blockmesh/133559-any-simple-way-view-blockmeshdict-vertex-numbers-indices.html)和[这里](https://openfoamwiki.net/index.php/BlockMesh)，可用 `blockMesh` 生成一 obj 文件，该 obj 文件中节点的顺序和 blockMeshDict 中指定的是一样的，这样再由 `objToVTK` 生成vtk文件来交由 ParaView (这里使用的是 ParaView 5.0.1)处理就可以了。

具体步骤为：

1.使用 `blockMesh` 命令生成 obj 文件：
{% highlight bash %}
blockMesh -blockTopology
{% endhighlight %}
这样会生成两个 obj 文件：blockCentres.obj 和 blockTopology.obj ，我们只需要 blockTopology.obj

2.使用 `objToVTK` 将 obj 文件转为 vtk 文件：
{% highlight bash %}
objToVTK blockTopology.obj blockTopology.vtk
{% endhighlight %}

3.用 ParaView 打开 blockTopology.vtk 并选中所有节点(按 d 键，然后框选整个结构)

4.使用 ParaView 的 View 菜单，打开 Selection Display Inspector ，并将 Selection Display Inspector 里面 Point Labels 选为 pointID ，这样显示的节点编号为浮点数，如0.000000等，需要进一步设置一下

5.点击 Selection Display Inspector 中 Selection Color 后面的小齿轮(设置)，打开 Selection Label Properties 并将 Point Label Format 设置为 %2g 等 `printf` 的格式就可以了，其它颜色啥的自己看着调下就行

显示出来节点的编号我们就可以对照着 blockMeshDict 来查看 face 的构成，block 的构成了。使用 `blockMesh` 时要求 blockMeshDict 是一个完整的 (vertices, blocks, boundary 等应该都要有)，但 blocks, boundary 的内容可以为空，故而可用这种方法来辅助我们写 blockMeshDict。

