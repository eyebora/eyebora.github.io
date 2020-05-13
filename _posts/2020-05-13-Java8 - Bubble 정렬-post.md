---


---

<h1 id="java8-bubble-정렬">Java8 Bubble 정렬</h1>
<h2 id="개요">1. 개요</h2>
<p>Java8 Stream 클래스를 활용하여 Bubble 정렬을 구현.<br>
Bubble 정렬이란? 인접한 2개의 요소를 중첩되게 비교하여  정렬하는 방식입니다.</p>
<h2 id="처리절차">2. 처리절차</h2>
<p>배열을 정렬하기 위해 인접한 요소를 비교하고 필요한 경우 교체하면서 배열을 반복합니다. 크기가 <em>n</em> 인 배열의 경우 <em>n-1</em> 개의 반복을 수행합니다.</p>
<p>배열을 오름차순으로 정렬하고 싶습니다.</p>
<p>4 2 1 6 3 5</p>
<p>4와 2를 비교하여 첫 번째 반복을 시작합니다.</p>
<p><strong>[2 4]</strong> 1 6 3 5</p>
<p>이제 4와 1에 대해 동일하게 반복합니다.</p>
<p>2 <strong>[1 4]</strong> 6 3 5<br>
2 1 <strong>[4 6]</strong> 3 5<br>
2 1 4 <strong>[3 6]</strong> 5<br>
2 1 4 3 <strong>[5 6]</strong></p>
<p>여기까지 오면 가장 큰수가 가장 우측에 배치하게 되며, 다시 n-1 까지 비교합니다.</p>
<p><strong>[1 2]</strong> 4 3 5 6<br>
1 <strong>[2 4]</strong> 3 5 6<br>
1 2 <strong>[3 4 ]</strong> 5 6<br>
1 2 3 <strong>[4 5]</strong> 6</p>
<p><em>n-1</em> 반복 이 끝나면 오름차순으로 정렬 된 배열을 얻을 수 있습니다.</p>
<h2 id="구현">3. 구현</h2>
<p>Java8 Stream을 사용하여 Bubble 정렬된 소스입니다.</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">BubbleSort</span> <span class="token punctuation">{</span>	
	<span class="token keyword">public</span> <span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token function">execute</span><span class="token punctuation">(</span> <span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> arr <span class="token punctuation">)</span> <span class="token punctuation">{</span>
	    <span class="token keyword">int</span> n <span class="token operator">=</span> arr<span class="token punctuation">.</span>length<span class="token punctuation">;</span>
	    IntStream<span class="token punctuation">.</span><span class="token function">range</span><span class="token punctuation">(</span><span class="token number">0</span><span class="token punctuation">,</span> n <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">)</span>
	    <span class="token punctuation">.</span><span class="token function">flatMap</span><span class="token punctuation">(</span>i <span class="token operator">-</span><span class="token operator">&gt;</span> IntStream<span class="token punctuation">.</span><span class="token function">range</span><span class="token punctuation">(</span><span class="token number">1</span><span class="token punctuation">,</span> n <span class="token operator">-</span> i<span class="token punctuation">)</span> <span class="token punctuation">)</span>
	    <span class="token punctuation">.</span><span class="token function">forEach</span><span class="token punctuation">(</span>j <span class="token operator">-</span><span class="token operator">&gt;</span> <span class="token punctuation">{</span>
	        <span class="token keyword">if</span> <span class="token punctuation">(</span>arr<span class="token punctuation">[</span>j <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">]</span> <span class="token operator">&gt;</span> arr<span class="token punctuation">[</span>j<span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	            <span class="token keyword">int</span> temp <span class="token operator">=</span> arr<span class="token punctuation">[</span>j<span class="token punctuation">]</span><span class="token punctuation">;</span>
	            arr<span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token operator">=</span> arr<span class="token punctuation">[</span>j <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
	            arr<span class="token punctuation">[</span>j <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">]</span> <span class="token operator">=</span> temp<span class="token punctuation">;</span>
	            <span class="token punctuation">}</span>
	     <span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	    <span class="token keyword">return</span> arr<span class="token punctuation">;</span>
	<span class="token punctuation">}</span> 
<span class="token punctuation">}</span>
</code></pre>
<p>테스트 코드</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">class</span> <span class="token class-name">BubbleSortTests</span> <span class="token punctuation">{</span>	
	<span class="token annotation punctuation">@Test</span>
	<span class="token keyword">public</span> <span class="token keyword">void</span> <span class="token function">_Test_execute</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>		
		<span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> array <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token punctuation">{</span> <span class="token number">3</span><span class="token punctuation">,</span><span class="token number">7</span><span class="token punctuation">,</span><span class="token number">8</span><span class="token punctuation">,</span><span class="token number">5</span><span class="token punctuation">,</span><span class="token number">4</span> <span class="token punctuation">}</span><span class="token punctuation">;</span>
		<span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> sortedArray <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token punctuation">{</span> <span class="token number">3</span><span class="token punctuation">,</span><span class="token number">4</span><span class="token punctuation">,</span><span class="token number">5</span><span class="token punctuation">,</span><span class="token number">7</span><span class="token punctuation">,</span><span class="token number">8</span> <span class="token punctuation">}</span><span class="token punctuation">;</span>		
		BubbleSort bubbleSort <span class="token operator">=</span> <span class="token keyword">new</span> <span class="token class-name">BubbleSort</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>		
		array <span class="token operator">=</span> bubbleSort<span class="token punctuation">.</span><span class="token function">execute</span><span class="token punctuation">(</span> array <span class="token punctuation">)</span><span class="token punctuation">;</span>	
		<span class="token function">assertThat</span><span class="token punctuation">(</span>array<span class="token punctuation">,</span> <span class="token function">is</span><span class="token punctuation">(</span>sortedArray<span class="token punctuation">)</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token punctuation">}</span>
<span class="token punctuation">}</span>
</code></pre>
<h2 id="시간-복잡도">4. 시간 복잡도</h2>
<p>최악의 경우 시간복잡도(Time Complexity) 는 O(n^2)<br>
공간복잡도는 Swap을 하기 위한 1개 따라서 O(1)<br>
또한 알고리즘을 살펴보면 내부 루프에서 교환이 한번도 없는 경우는 이미 정렬이 되었다고 판단할 수 있습니다.<br>
이대는 시간복잡도 O(n) 이 됩니다.</p>
<p>최적화된 코드(한번도 교환이 없는 경우 적용)</p>
<pre class=" language-java"><code class="prism  language-java"><span class="token keyword">public</span> <span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> <span class="token function">optimizedBubbleSort</span><span class="token punctuation">(</span><span class="token keyword">int</span><span class="token punctuation">[</span><span class="token punctuation">]</span> arr<span class="token punctuation">)</span> <span class="token punctuation">{</span>
	    <span class="token keyword">int</span> i <span class="token operator">=</span> <span class="token number">0</span><span class="token punctuation">,</span> n <span class="token operator">=</span> arr<span class="token punctuation">.</span>length<span class="token punctuation">;</span>
	    <span class="token keyword">boolean</span> swapNeeded <span class="token operator">=</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
	    <span class="token keyword">while</span> <span class="token punctuation">(</span>i <span class="token operator">&lt;</span> n <span class="token operator">-</span> <span class="token number">1</span> <span class="token operator">&amp;&amp;</span> swapNeeded<span class="token punctuation">)</span> <span class="token punctuation">{</span>
	        swapNeeded <span class="token operator">=</span> <span class="token boolean">false</span><span class="token punctuation">;</span>
	        <span class="token keyword">for</span> <span class="token punctuation">(</span><span class="token keyword">int</span> j <span class="token operator">=</span> <span class="token number">1</span><span class="token punctuation">;</span> j <span class="token operator">&lt;</span> n <span class="token operator">-</span> i<span class="token punctuation">;</span> j<span class="token operator">++</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	            <span class="token keyword">if</span> <span class="token punctuation">(</span>arr<span class="token punctuation">[</span>j <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">]</span> <span class="token operator">&gt;</span> arr<span class="token punctuation">[</span>j<span class="token punctuation">]</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
	                <span class="token keyword">int</span> temp <span class="token operator">=</span> arr<span class="token punctuation">[</span>j <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">]</span><span class="token punctuation">;</span>
	                arr<span class="token punctuation">[</span>j <span class="token operator">-</span> <span class="token number">1</span><span class="token punctuation">]</span> <span class="token operator">=</span> arr<span class="token punctuation">[</span>j<span class="token punctuation">]</span><span class="token punctuation">;</span>
	                arr<span class="token punctuation">[</span>j<span class="token punctuation">]</span> <span class="token operator">=</span> temp<span class="token punctuation">;</span>
	                swapNeeded <span class="token operator">=</span> <span class="token boolean">true</span><span class="token punctuation">;</span>
	            <span class="token punctuation">}</span>
	            System<span class="token punctuation">.</span>out<span class="token punctuation">.</span><span class="token function">println</span><span class="token punctuation">(</span>j<span class="token punctuation">)</span><span class="token punctuation">;</span>
	        <span class="token punctuation">}</span>
	        i<span class="token operator">++</span><span class="token punctuation">;</span>
	    <span class="token punctuation">}</span>
	    <span class="token keyword">return</span> arr<span class="token punctuation">;</span>
	<span class="token punctuation">}</span>
</code></pre>
<h2 id="결론">4. 결론</h2>
<ul>
<li>최악의 경우 : 배열이 역순 일 때 O (n * n)</li>
<li>최선의 경우 : 배열이 이미 정렬 된 경우 O (n)</li>
</ul>
<p><strong>최선의 경우를 적용하여 최적화된 버블Sort를 구현</strong></p>
<blockquote>
<p>작성자 : <a href="https://github.com/eyebora">eyebora32</a><br>
참조 : <a href="https://www.baeldung.com/java-bubble-sort">https://www.baeldung.com/java-bubble-sort</a><br>
Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>

