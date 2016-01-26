# getbem-faq-CHS-
FAQ of getbem.com in Chinese
#FAQ#
这些频繁被问到的问题是刚刚开始使用BEM的开发者们真实遇到的问题，由GetBEM社区来回答。请不要客气地的随便提问，然后我们也会解答。

-	为什么我要选择BEM而不是其他的CSS模块（block)化解决方案？
-	为什么修饰符(modifier)的CSS类们不能用联合选择器来代表？ 
-	为什么我需要用块（block)的CSS类来代替使用语义化的定制标签？ 
-	为什么我需要同时使用块（block)和带前缀的修饰符来定义修饰符块（block)？ 
-	一个块（block)修饰符能不能影响元素？ 
-	我能不能创建一个全局的修饰符(modifier)来适用于任意一个块（block)(block)？ 
-	我能不能联合一个标签和一个类在选择器里，就像button.button？ 
-	通过其CSS内容来命名修饰符这样好吗？比如 .block__element--border-bottom-5px 
-	当一个元素嵌套在另一个元素里面，应该怎么命名？比如 block__elem1__elem2？ 
-	我听说BEM不推荐全局CSS reset ？为什么？ 
-	没有找到答案？ 


###为什么我要选择BEM而不是其他的CSS模块（block)化解决方案？###

>有一些其他的CSS的模块（block)化解决方案（比如OOCSS,AMCSS,SMACSS,SUITCSS)。我们选择BEM的原因是什么。

BEM为所有的前端技术提供了解决方案：CSS,JavaScript,templating(模板），也有web应用的建立过程。这个方法论适用于任何地方。虽然让这个方法论适用于JavaScript和templating的时候你需要专门的框架，但是用在CSS的时候你可能只需要依照推荐的方法。CSS部分是BEM里最简单的能应用在你的开发过程中的。这就是为什么很多人只用这一部分。另一方面，如果你近来发现你的项目充分的使用了BEM并且你自己因为维护而开心，你大概就准备进行下一步来模块（block)化的你的web应用了。BEM CSS可以更简单的调整模块（block)化JavaScript 和基于块（block)的项目文件结构

如果只谈CSS模块（block)化解决方案，BEM特色的关键是块（block)的相互独立。依据CSS的建议，可以把一个块（block)放到任意一个页面的任意位置并且可以确保它不会被它周围的东西所影响。并且，如果你需要嵌套另一个块（block)到现有的一个块（block)，他们的整体兼容性是可以保证的。换一句话说，当维持你的Web应用的时候，你可以跨页面移动块（block)，添加其他的块（block)并结合他们。

BEM CSS 明确的定义了哪个CSS属于界面的哪一块（block)。所以他回答诸如“我能不能移动这里的代码？”，“如果我更改这里的代码那么会发生什么，页面哪部分会受到影响？”这些问题。

###为什么修饰符(modifier)的CSS类们不能用联合选择器来代表？###

>BEM 推荐像 `<div class="block block--mod">` 这样来修饰一个块（block)，为什么不使用简单的版本像 `<div class="block mod">`？既然我们已经联合了选择器 `.block.mod`，那么依此定义所有的CSS都不难。

推荐把修饰符的CSS用它的块（block)名来加前缀有多重原因。

第一，因为有可能在同一个DOM节点混合使用几个块（block)和元素，我们需要保证一个修饰符仅仅只影响它属于的块（block)。让我们假设这里有一个menu item和一个button混合在一起。在HTML里这种构筑表现的像下面这样。

`<div class="menu__item button"></div>`

在这种情况下，增加`.active`修饰符给他们会影响二者。

`<div class="menu__item button active"></div>`

所有这三者都在同样的一个DOM节点里，所有不可能去区分我们的意思是`menu__item.active`还是`button.active`。<br>然而在有前缀的情况下，命名`button--active` 明确的说明了这个只是影响了 button这个块（block)。

另外一个重点是CSS的specificity（特异性）。联合的选择器比单一类选择器更加特殊（意思是更加重要）。这意味着你可能会遇到麻烦当用parent块（block)的代码来重新定义他们的时候。

	<div class="header">
		<button class="button active">
	</div>

如果你已经有了`.button.active` 选择器在代码里了，那么重新定义`.header.button`的specificity（特异性）和联合修饰符的选择器的specificity（特异性）是完全相同的，这取决于CSS规则声明的顺序。然而为了防备使用了有前缀的修饰符，你可以一直确使自己使用的层叠选择器`.header .button`会覆盖`.button--active`修饰符。

这会让生命更加容易，尤其是对于可维持的项目。

第三点是看看这个代码`<div class="block block--mod">` ，你可以清晰的看出块（block)的结构。很容易认出这个块（block)以及它的修饰符，也没什么需要解释的。不幸的是这个代码`<div class="block mod">`并没有给出什么信息。基于复杂的CSS类，有时候并不可能去辨认出我们是否在这里有一个块（block)和一个修饰符还是有两个块（block)。这甚至可能更加混乱如果实体的名字很复杂或者很简短（这是有时候在大的项目里发生的）<br>对块（block)的结构清楚的理解对我们在文件系统里寻找一致的代码十分有帮助。

你也会感激`.block--mod`的使用当重构和使用全局搜索在你的项目文件的时候。想想一下同样是寻找没用前缀的`.mod`在所有HTML文件的情景。

最后，站在一个开发过程的立场，`.block.mod`和`.block--mod`唯一区别就是他们的符号用 `-`代替了 `.` ，这什么都没有花费就给你带来了上述的好处。此外，因为预处理机开始支持BEM符号了，那么相当的自然去写`&--mod`，并得到一个修饰符声明像推荐的一样。

###为什么我需要用块（block)的CSS类来代替使用语义化的定制标签？ ###

>块（block)可以被CSS规则定义的定制的标签来代表，所有看上去我们一点也不需要CSS类来代表块（block)。他们可以只用修饰符，就像`<button class="mod"/>`

使用定制的标签作为块（block)选择器确实是BEM下的一种解决方案，然而这种变体比推荐的“class"方法少了一些灵活性。

看上去你需要加块（block)名前缀的修饰符类来提供他们的命名空间，细节你可以看看“为什么修饰符(modifier)的CSS类们不能用联合选择器来代表？”这个问题。所以，最后的这个块（block)的定制标签版本就像`<block class="block--mod"/>`。这个看上去和`<div class="block block--mod">`区别并不大，尤其是假设标签独立，你可以使用任意定制的节点并坚持使用`<block class="block block--mod">`

第二个缺点是，“标签”版本让混合使用块（block)变得不可能，然而"类"版本表现的自然比如 `<div class="block1 block2">`

最后的反对意见是，在许多情况下，你不能把你的块（block)表现的全部像一个定制的标签。比如一个`link`的块（block)你清楚的需要一个`<a>`标签，同样还有`<input>`。

###为什么我需要同时使用块（block)和带前缀的修饰符来定义修饰符块（block)？ ###

>为什么块（block)和修饰符的类要放在一起，在同一个修饰符块（block)比如`<div class="block block--mod">`？

>关于修饰符块（block)的所有内容都可以描述在 `.block--mod`。如果两个修饰符里有一些共同的东西，那么可以用预处理器去消除复制粘贴的问题。

这个方法的可能性要感谢预处理器。然而这却带来了一些缺点，你应该意识到。

为了防止两个或更多修饰符在同一个块（block) `<div class="block--theme--christmas block--size--big">`，你可能得到了两次块（block)样式的核心内容。这取决于预处理器的算法。

当使用JavaScript动态的操作修饰符的时候，那么附加的修饰符就会容易。转换它意味着仅仅从DOM节点移除一个CSS类，而不需要增加block的核心CSS 因为这个类一直在这里。

###一个块（block)修饰符能不能影响元素？###

>如果我有一个块（block)修饰符，比如`xmas`,然后我想要一个在这个块（block)里的元素也有这个修饰 ，那么我最好该怎么做。

>把`--xmas`这个后缀加到每一个元素的后面必要吗？还是应该把这一个用例来嵌套进去。（e.g `block--xmas block__elem{...}`?）

尽管总的来说BEM建议避免嵌套选择器，但是这种情况是合理的。

当创建嵌套的选择器的时候，你就声明了一个实体依靠于另外一个。因为 BEM采用的是独立的组件，这样的一个方法在我们说两个不同的块（block)的时候并不建议。

但是当他们是一个块（block)和它的元素的时候，他们并不是等价的含义。根据定义，一个元素没用任何意义当它脱离了它的块（block)。所以，一个元素是一个块（block)依赖的实体。明白了这个，那么一个元素被它的块（block)现有的状态影响就很正常且合乎逻辑了。

所以，这完全是一个BEM的代码模式。

	.my-block--xmas .my-block__button {
	    /* Jingle bells, jingle bells, jingle all the way.*/
	}

###我能不能创建一个全局的修饰符(modifier)来适用于任意一个块（block)(block)？###

>我听说全局的修饰符比如`visible`,`invisible`,`red`,`opacity50` 再BEM里并不受欢迎，为什么？

>我认为包含这些共通的属性在这样的全局类里，然后让他们适用于不同的块（block)比较实用。

确实你可以有两个主要CSS类再相同的DOM节点里，在BEM里我们叫它 `mix`:

`<div class="block1 block2"></div>`

但是重要的事情是，`block1`和`block2`都应该是单独的块（block)。这和人们经常意指的没有任何含义而仅仅是设置属性变更的“全局修饰符”有轻微的区别，

`<div class="block globalmod"></div>`

如果你认为你的情况你会有一个全局修饰符，那么这些问题你有可能会遇到。

第一，specificity（特异性）的问题会出现。在局部的情况CSS的代码像这样。

	.block {
	  display: block;
	}
	.block--hidden {
	  display: none;
	}

块（block)和修饰符选择器有相同的specificity（特异性）。因为修饰符声明在块（block)的后面，所有重新定义了CSS的属性。这些样式属于块（block)并且存储在了块（block)文件中。因此，在源文件编译的结果里，你一直会得到他们按照这个顺序，并且可以确定重定义的发生。

在全局修饰符的情况下，它的属性们可以被块（block)们重定义，如果块（block)的代码在修饰符之后：

	.hidden { display: none }
	/* ... */
	.block { display: block }

`<div class="block hidden">you still see me</div>`

一个针对这个问题的可能的解决方案是通过使用`!important`提升全局修饰符的选择器的specificity。但是这样也会出现副作用，那就是只有同样声明了`!important`的指令才可以覆盖它。

另外一个方法在加载了所有其他样式后再读取全局修饰符的CSS。但是这种情况你不能再为你的其他组件使用延迟加载（lazy boading)的方法。因为额外的延迟CSS会仍然在你的修饰符之后加载，然后就会出现同样的问题。

下一个问题是结合多个全局修饰符在同一个块（block)里。

`<div class="block mod1 mod2"></div>`

在这种情况下你绝对不能完全支配这个块（block)。修饰符在代码里的顺序不同，如果和其他爱的生命冲突了，更改顺序可以解决这个冲突但是会导致另外一个。唯一的办法是重定义这些块（block)里的混乱。别忘了对你的hack用`!important`。

同时，基于不同的块（block)，同一个修饰符也可能执行的不同。即使是一个简单的`.hidden`,有时候需要的不是`display:none`而是`visibility:hidden`，甚至是`position: absolute(绝对的); left: -9999px`等等，如果你需要在你的块（block)里做一些修改，那么更好的不是浪费时间在所有的地方来寻找可以和这个块（block)联合的全局修饰符，尤其是这种修饰关系并没有在很多地方使用。

所有这种地狱般的情况通过把一个修饰符封装进块（block)如`.block--mod`来避免。

确实使用全局修饰符可以让最后的代码变少，但是如果你用bytes测量真正的不同，它看上去并没有那么大。尤其是你使用联合选择器使CSS最优化。

###我能不能联合一个标签和一个类在选择器里，就像`button.button?` ###

>我想使用选择器像`button.button`来把我的块（block)的功能封装到一个特别的标签里。这样如果别人使用他们的代码`<h2 class="button">`，这样的一个封装可以防止冲突。

这样一个选择器的CSS specificity(特异性) `.button--mod`选择器并不会覆盖块（block)CSS属性，只有当`button.button--mod`才会有用。你会需要它的标签结合它的修饰符，而且其他开发者也会需要当他们重定义你的块（block)的时候。

当一个项目变大的时候，很可能你会有`input.button`,`span.button`和`a.button`，这所有的加前缀后的修饰符选择器和嵌套的元素都需要4个声明。

所以还是不要把你的手用去加前缀比较好，但是如果你仍然可以保证你的块（block)用在适当的标签下，如果你提供给你的使用者每个块（block)的模板，那么这是最灵活的和必然的解决方案。

如果模板看上去很难，那么可以用“文档”的方法来告诉你的使用者块（block)CSS类应用于哪个标签，文档记录块（block)代码可以完成这些。最短版本可以仅仅用注释的方式把标签名称加到块（block)生命的前面`/*button*/.button',或者可以是很长的注释评论在HTML里，块（block)作用的地方。

###通过其CSS内容来命名修饰符这样好吗？比如 .block__element--border-bottom-5px ###

>感谢mixes,我们可以创建很多修饰符来代表CSS的属性，并且分配他们到块（block)里。但是我听说这并不好。比如，这样的选择器`block__element--border-bottom-5px`是被称为很可怕的。我在想为什么还有如何命名修饰符呢？

命名修饰符使其和他们CSS代表一致并不推荐。确实它看上去很好但是这里也有很多实用性的原因来反对它。比如你近来改变了你的组件的视图，那么你需要修正的不仅仅是CSS内容，还有选择器。所以，你把border改成6px，那么你需要修改所有的模板有时甚至包括JavaScript。

并且，从来没有发生过一个修饰符仅仅定义一个CSS属性并且永远只有它。即使现在它只有一个border用来区分一个状态，这很可能你需要其他CSS属性来修饰你这个块（block)里的同一个状态。如果你在一个叫"border"的修饰符里定义一个background或者padding可能会让代码变得凌乱。所以，推荐使用语义化的修饰符命名即使现在只有一个属性。

###当一个元素嵌套在另一个元素里面，应该怎么命名？比如 `block__elem1__elem2`###

>如果我的块（block)有一个复杂的结构，它的元素相互嵌套，我应该怎么办？CSS类像`block__elem1__elme2__elem3`看着很恐怖。

根据BEM理论，块（block)的结构是应该被扁平。你不需要反映出块（block)的DOM结构的嵌套关系，所有，在这种情况下这些类命名应该是:

	.block {}
	.block__elem1 {}
	.block__elem2 {}
	.block__elem3 {}

然而DOM表现在块（block)里是嵌套的:

	<div class='block'>
	    <div class='block__elem1'>
	        <div class='block__elem2'>
	            <div class='block__elem3'></div>
	        </div>
	    </div>
	</div>

除此之外的事实是，这些类看着更加好看了，这让这些元素仅仅依靠块（block)。所以，假如你需要更改页面，你可以轻易的穿越块（block)来移动这些元素。这些块（block)DOM结构的改变不需要对应的CSS代码的改变。
	
	<div class='block'>
		<div class='block__elem1'>
			<div class='block__elem2'></div>
		</div>
		<div class='block__elem3'></div>
	</div>

###我听说BEM不推荐全局CSS reset ？为什么？###

>实践证明CSS resets有不错的效果，许多框架先把一切东西先对齐，然后再应用特定的样式。BEM不推荐用共通的resets.为什么？那么我们假定了什么来代替它？

如果你使用共通的reset其实并不会有什么坏事发生在你的块（block)上(好吧，除了下面的特殊的情况)。所以，BEM不阻止你使用它们。但是使用它们按照BEM的方式会更加有效。

共通的CSS reset是一个应用于文档节点的CSS设置，它保证了即使在不同的浏览器下这些节点也有相同的默认视图。在大多数情况下这些CSS规则被写给标签选择器，这样BEM并不推荐（你可以在上面找到解释）

另外一个关键点是在BEM中，块（block)压缩了所有它在表现和作用时需要的东西。这就是我们为什么称BEM的块（block)是独立的。如果块（block)离开了页面添加的第三方CSS就看着不那么正确了，那么就不能把它更多的称为“独立”了。

在这种前提下，BEM推荐每个块（block)来reset自己。如果你在你的HTML里有`menu`块（block)和`list`块（block)，并且都是`<ul>`。那么他们每一个分别要提供一个通常提供给`<ul>`的reset。你可能会担心几个块（block)有相同的reset规则而造成重复以致代码的冗余。但是这是CSS 优化器需要帮你做的。作为一个开发人员，你开发每个块（block)独立的，因为在同一个页面不会有其他的块（block)。

在你没有CSS优化器来联合选择器处理相同的代码时，你可以使用预处理器来阻止copy-paste。对每一个新的块（block)，你都可以让他通过混合适当的代码reset自己，使用SASS就会看着像这样：

	.menu {
	    @include reset-list;
	}
	.menu__item {
	    @include reset-list-item;
	}

	/* ... */

	.list {
	    @include reset-list;
	}
	.list__item {
	    @include reset-list-item;
	}

然而使用这种混合的方式的时候你需要意识到你这么做的唯一原因是因为没有一个合适的优化器。

为每个块（block)reset（除了更好看和更加BEM化），也会阻止注入那些依靠浏览器默认值的第三方的HTML/CSS markup来影响全局resets的问题。举个例子就是，webmails的问题。

