---
layout: post
title: "C++ Fallacies: Pre vs Post Increment Efficiency"
date: 2013-08-29 17:50
comments: true
published: false
tags: ['c++', 'post-increment', 'pre-increment', 'fallacies']
---

One of the most common C/C++ fallacies I hear (from new and experienced programmers alike) is that it's faster to use the pre-increment operator than the post-increment operator in for loops. In theory, this make sense. Here is how pre-increment would typicaly be defined:

    int pre_increment(int &x) {
        x += 1;
        return x;
    }

And here's how post-increment would typically be defined:

    int post_increment(int &x) {
        int ret = x;
        x += 1;
        return ret;
    }

We can see that more work needs to be done in `post_increment` function, and when used in a for loop the amount of wasted time might add up. In practice, however, most compilers optimize this away (even without explicitly turning on optimizations). This true for the GNU C/C++ compiler, and, while I haven't tested it with other compilers, it should be true for every modern compiler (and if you ever find that it's not, it's time to ditch your compiler).

Consider the following code snippets. The return value is needed, so let's look at the assembly code generated and the time it takes to execute each snippet:

    #include <iostream>

    using std::cout;
    using std::endl;

    int main() {
        int x = 1;
        int y;

        for (int i = 0; i < 1000000000; i++) {
            y = x++;
        }

        cout << x << endl;
    }
