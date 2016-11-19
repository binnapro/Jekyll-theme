---
layout: post
title: "rc-form翻译"
subtitle: "translate document about rc-form"
date: 2016-11-01
author: "Binna"
header-img:
catalog: true
tags:
    - 文档翻译
    - npm包
---

# rc-form

[![npm](https://img.shields.io/npm/v/rc-form.svg?style=flat-square)](https://npmjs.org/package/rc-form)
[![build](https://img.shields.io/travis/react-component/form.svg?style=flat-square)](https://travis-ci.org/react-component/form)
[![coverage](https://img.shields.io/coveralls/react-component/form.svg?style=flat-square)](https://coveralls.io/r/react-component/form?branch=master)
[![dependencies](https://img.shields.io/gemnasium/react-component/form.svg?style=flat-square)](https://gemnasium.com/react-component/form)
[![nodejs](https://img.shields.io/badge/node.js-%3E=_0.10-green.svg?style=flat-square)](http://nodejs.org/download/)
[![download](https://img.shields.io/npm/dm/rc-form.svg?style=flat-square)](https://npmjs.org/package/rc-form)

## 展开

```shell
npm install
npm start
```

## 例子

在线例子：[https://react-component.github.io/form/examples/](https://react-component.github.io/form/examples/)

## 特点

* 支持reactjs，并且支持react-native

## 安装

![npm install rc-from](https://nodei.co/npm/rc-form.png)

## 用法

```javascript
import { createForm } from 'rc-form';

class Form extends React.Component {
  submit = () => {
    this.props.form.validateFields((error, value) => {
      console.log(error, value);
    });
  }

  render() {
    let errors;
    const { getFieldProps, getFieldError } = this.props.form;
    return (<div>
      <input {...getFieldProps('normal')}/>
      <input {...getFieldProps('required', {
        onChange(){}, // have to write original onChange here if you need
        rules: [{required: true}],
      })}/>
      {(errors = getFieldError('required')) ? errors.join(',') : null}
      <button onClick={this.submit}>submit</button>
    </div>)
  }
}

export createForm()(Form);
```

或者更快的用法：

```js
import { createForm } from 'rc-form';

class Form extends React.Component {
  componentWillMount() {
    this.requiredDecorator = this.props.form.getFieldDecorator({
        name: 'required',
        rules: [{required: true}],
    });
  },

  submit = () => {
    this.props.form.validateFields((error, value) => {
      console.log(error, value);
    });
  }

  render() {
    let errors;
    const { getFieldError } = this.props.form;
    return (<div>
      {this.requiredDecorator(
      <input onChange={
      // can still write your own onChange }
      />)}
      {(errors = getFieldError('required')) ? errors.join(',') : null}
      <button onClick={this.submit}>submit</button>
    </div>)
  }
}

export createForm()(Form);
```

## createForm(formOption):Function

### formOption.vaildateMessages:object





