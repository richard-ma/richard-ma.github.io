---
layout: post
category: source-reading 
title: cs-cart 模块初始化函数列表 
tags: cs-cart
---

# 模块初始化函数

模块初始化函数名（按加载顺序）  |初始化条件
--------------------------------|-------------------
fn_init_api                     | API常量已定义（开启API模式时）
fn_init_storage                 | *
fn_init_ua                      | *
fn_init_store_params_by_host    | fn_allowed_for('ULTIMATE')
Tygh-Session, init              | *
fn_init_ajax                    | *
fn_init_company_id              | *
fn_check_cache                  | *
fn_init_settings                | *
fn_init_addons                  | *
fn_get_route                    | *
fn_simple_ultimate              | *
fn_init_localization            | !fn_allowed_for('ULTIMATE:FREE')
fn_init_language                | *
fn_init_currency                | *
fn_init_company_data            | *
fn_init_full_path               | *
fn_init_layout                  | *
fn_init_user                    | *
fn_init_templater               | *

注：

* *表示没有限制条件，默认执行该模块初始化
* fn_allowed_for 查看当前的许可是否允许，比如是free还是full授权

# fn_allowed_for

* 授权许可文件储存在数据库中: storage_data表store_mode行
* free版本的授权文件为普通的文本文件，内容为free
