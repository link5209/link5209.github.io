---
published: true
title: down/up stream
layout: post
tags: [js]
categories: [js]
---
``` javascript

'use strict'

console.log('\n#mw downstream&upstream flow')

function topic(next) {
    console.log('-> topic')
    next()
    console.log('<- topic')
}

function module(next) {
    console.log('-> module')
    next()
    console.log('<- module')
}

function task(next) {
    console.log('-> task')
    console.log('<- task')

}

// primative way
let second = function() {
    module(task)
}
console.log('\n#primative way')
topic(second)
console.log()


// mw downstream&upstream flow
function compose(mws) {
    let i = mws.length-1
    let pre

    while (i >= 0) {
        pre = cons(mws[i--], pre)
    }
    return pre

    function cons(x, y) {
        return function() {
            x(y)
        }
    }
}

console.log('#dynamic way')
compose([topic, module, task])()

```