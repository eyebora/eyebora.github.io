---


---

<hr>
<h2 id="title-java8-heap-정렬date-2020-05-13-130000--0900categories-">title: “Java8 Heap 정렬”<br>
date: 2020-05-13 13:00:00 -0900<br>
categories: “”</h2>
<h1 id="java8-heap-정렬">Java8 Heap 정렬</h1>
<h2 id="개요">1. 개요</h2>
<p>Heap 정렬은 Heap Data Structure(자료구조) 를 기반으로 정렬을 수행합니다.  Heap Data Structure 를 정확히 이해하여 Heap정렬을 구현할 수 있습니다.</p>
<h2 id="heap-data-structure">2. Heap Data Structure</h2>
<p>Heap은 Tree형태의 Data Structure 입니다. Node로 구성되어 있으며 모든 Node는 한개의 Element를 가지고 있습니다. Node는 자식 Node를 가질 수 있으며, 자식이 없는 경우는 Leaf(잎)라고 부릅니다.</p>
<p>Heap 생성 규칙</p>
<ol>
<li>모든 노드의 값은 자식에 저장된 모든 값보다 작거나 같아야합니다</li>
<li>완전한 트리가 되기 위해서는 노드로 구성된 트리의 높이가 가장 작아야 합니다.</li>
</ol>
<blockquote>
<p>트리에서 가장 작은 값이 Root가 됩니다.</p>
</blockquote>
<h3 id="heap-확장하기">2.1 Heap 확장하기</h3>
<p>힙에는 많은 변형이 있으며 모두 구현 세부 사항이 다릅니다.</p>
<p>예를 들어, 위에서 설명한 것은 Min-Heap입니다. 부모는 항상 모든 자식보다 작기 때문입니다. 또는 Max-Heap을 정의 할 수 있습니다.이 경우 부모는 항상 자식보다 큽니다. 따라서 가장 큰 요소는 루트 노드에 있습니다.</p>
<p>많은 트리 구현 중에서 선택할 수 있습니다. 가장 간단한 방법은 Binary Tree(이진 트리)입니다. 이진 트리에서 모든 노드는 최대 두 개의 자식 노드(왼쪽 자식노드, 오른쪽 자식 노드)를 가질 수 있습니다.</p>
<p>두 번째 규칙을 적용하는 가장 쉬운 방법은 전체 이진 트리를 사용하는 것입니다. 전체 이진 트리는 몇 가지 간단한 규칙을 따릅니다.</p>
<blockquote>
<p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

