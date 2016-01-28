暂未翻译

官方文档[点此](https://docs.djangoproject.com/en/1.8/intro/tutorial05/)

---

# 创建你的第一个 Django 项目， 第五部分

这一篇从[第四部分（en）](part4.md)结尾的地方继续讲起。我们在前几章成功的构建了一个在线投票应用，在这一部分里我们将其创建一些自动化测试。

## 自动化测试简介

### 自动化测试是什么？

测试，是用来检查代码正确性的一些简单的程序。

测试在不同的层次中都存在。有些测试只关注某个很小的细节（某个模型的某个方法的返回值是否满足预期？），而另一些测试可能检查对莫个软件的一系列操作（某一用户输入序列是否造成了预期的结果？）。其实这和我们在教程的[第一部分(zh)](part1.md)里做的并没有什么不同，我们使用 [shell](https://docs.djangoproject.com/en/1.8/ref/django-admin/#django-admin-shell) 来测试某一方法的功能，或者运行某个应用并输入数据来检查它的行为。

真正不同的地方在于，自动化测试是由某个系统帮你自动完成的。当你创建好了一系列测试，每次修改应用代码后，就可以自动检查出修改后的代码是否还像你曾经预期的那样正常工作。你不需要话费大量时间来进行手动测试。

### 为什么你需要写测试

但是，为什么需要测试呢？又为什么是现在呢？

你可能觉得学 Python/Django 对你来说已经很充实了，再学一些新东西的话看起来有点负担过重并且没什么必要。毕竟，我们的投票应用看起来已经完美工作了。写一些自动测试并不能让它工作的更好。如果写一个投票应用是你想用 Django 完成的唯一工作，那你确实没必要学写测试。但是如果你还想写更复杂的项目，现在就是学习测试写法的最好时机了。

### 测试将节约你的时间

在某种程度上，能够「判断出代码是否正常工作」的测试，就称得上是个令人满意的了。

在更加复杂的应用中，各种组件之间的交互可能会及其的复杂。改变其中某一组件的行为，也有可能会造成意想不到的结果。判断「代码是否正常工作」意味着你需要用大量的数据来完整的测试全部代码的功能，以确保你的小修改没有对应用整体造成破坏——这太费时间了。

尤其是当你发现自动化测试能在几秒钟之内帮你完成这件事时，就更会觉得手动测试实在是太浪费时间了。当某人写出错误的代码时，自动化测试还能帮助你定位错误代码的位置。

有时候你会觉得，和富有创造性和生产力的业务代码比起来，编写枯燥的测试代码实在是太无聊了，特别是当你知道你的代码完全没有问题的时候。

然而，编写测试还是要比花费几个小时手动测试你的应用，或者为了找到某个小错误而胡乱翻看代码要有意义的多。

### 测试不仅能发现错误，而且能预防错误

「测试是开发的对立面」，这种思想是不对的。

如果没有测试，整个应用的行为意图会变得更加的不清晰。甚至当你在看自己写的代码时也是这样，有时候你需要仔细研读一段代码才能搞清楚它有什么用。

而测试的出现改变了这种情况。测试就好像是从内部仔细检查你的代码，当有些地方出错时，这些地方将会变得很显眼——就算你自己没有意识到那里写错了。

### 测试使你的代码更加诱人

你也许遇到过这种情况：你编写了一个绝赞的软件，但是其他开发者看都不看它一眼，因为它缺少测试。没有测试的代码不值得信任。 Django 最初开发者之一的 Jacob Kaplan-Moss 说过：“项目规划时没有包含测试是不科学的。”

其他的开发者希望在正式使用你的代码前看到它通过了测试，这是你需要写测试的另一个重要原因。

### 测试有利于团队协作

前面的几点都是从单人开发的角度来说的。复杂的应用可能由团队维护。测试的存在保证了协作者不会不小心破坏了了你的代码（也保证你不会不小心弄坏他们的）。如果你想作为一个 Django 程序员谋生的话，你必须擅长编写测试！

## 基础测试策略