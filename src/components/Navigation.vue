<template>
  <nav>
    <ul>
      <li><a href="#">Top</a></li>
      <li><a href="#">About</a></li>
      <li class="has-child">
        <a href="#">Service</a>
        <ul>
          <li><a href="#">Service Top</a></li>
          <li><a href="#">Service-1</a></li>
          <li class="has-child">
            <a href="#">Service-2</a>
            <ul>
              <li><a href="#">Service-2 Top</a></li>
              <li><a href="#">Service-2-1</a></li>
            </ul>
          </li>
          <li><a href="#">Service-3</a></li>
        </ul>
      </li>
    </ul>
  </nav>
</template>

<script setup>
  import { onMounted } from '@vue/runtime-core';
  import $ from 'jquery';

  onMounted(() => {
    function mediaQueriesWin() {
      const width = $(window).width();
      if (width <= 768) {
        $('.has-child>a').off('click');
        $('.has-child>a').on('click', function () {
          const parentElem = $(this).parent();
          $(parentElem).toggleClass('active');
          $(parentElem).children('ul').stop().slideToggle(500);
        });
        return false;
      } else {
        $('.has-child>a').off('click');
        $('.has-child>a').removeClass('active');
        $('.has-child').children('ul').css('display', '');
      }
    }

    $(window).on('resize', function () {
      mediaQueriesWin();
    });

    $(window).on('load', function () {
      mediaQueriesWin();
    });
  });
</script>

<style scoped>
  /* ナビゲーション全体の設定 */
  nav {
    background: #333;
    color: #fff;
    text-align: center;
  }
  /* 1階層目のナビゲーションを横並びにする */
  nav ul {
    display: flex;
    justify-content: center;
    list-style: none;
  }
  /* 2階層目以降は横並びにしない */
  nav ul ul {
    display: block;
  }
  /* 下の階層のulや矢印の基点にするため1階層目のli要素にrelativeを設定 */
  nav ul li {
    position: relative;
  }
  /* ナビゲーションのリンク関連 */
  nav ul li a {
    display: block;
    text-decoration: none;
    color: #999;
    padding: 20px 35px;
    transition: all 0.3s;
  }
  nav ul li li a {
    padding: 10px 35px;
  }
  nav ul li a:hover {
    color: #fff;
  }
  /* 矢印の設定 */
  /* 2階層目を持つliの矢印の設定 */
  nav ul li.has-child::before {
    content: '';
    position: absolute;
    left: 15px;
    top: 25px;
    width: 6px;
    height: 6px;
    border-top: 2px solid #999;
    border-right: 2px solid #999;
    transform: rotate(135deg);
  }
  /* 3階層目を持つliの矢印の設定 */
  nav ul ul li.has-child::before {
    content: '';
    position: absolute;
    left: 6px;
    top: 17px;
    width: 6px;
    height: 6px;
    border-top: 2px solid #fff;
    border-right: 2px solid #fff;
    transform: rotate(45deg);
  }
  /* 2・3階層目の共通設定 */
  nav li.has-child ul {
    /* 絶対配置で位置を指定 */
    position: absolute;
    left: 0;
    top: 64px;
    z-index: 4;
    /* 形状を指定 */
    background: #28bfe7;
    width: 180px;
    /* はじめは非表示 */
    visibility: hidden;
    opacity: 0;
    /* アニメーション設定 */
    transition: all 0.3s;
  }
  /* hoverしたら表示 */
  nav li.has-child:hover > ul,
  nav li.has-child ul li:hover > ul,
  nav li.has-child:active > ul,
  nav li.has-child ul li:active > ul {
    visibility: visible;
    opacity: 1;
  }
  /* ナビゲーションaタグの形状 */
  nav li.has-child ul li a {
    color: #fff;
    border-bottom: 1px solid rgba(255, 255, 255, 0.6);
  }
  nav li.has-child ul li:last-child a {
    border-bottom: none;
  }
  nav li.has-child ul li a:hover,
  nav li.has-child ul li a:active {
    background: #3577ca;
  }
  /* 3階層目 */
  /* 3階層目の位置 */
  nav li.has-child ul ul {
    top: 0;
    left: 182px;
    background: #66adf5;
  }
  nav li.has-child ul ul li a:hover,
  nav li.has-child ul ul li a:active {
    background: #448ed3;
  }
  /* 768px以下の形状 */
  @media screen and (max-width: 768px) {
    nav {
      padding: 0;
    }
    nav ul {
      display: block;
    }
    nav li.has-child ul,
    nav li.has-child ul ul {
      position: relative;
      left: 0;
      top: 0;
      width: 100%;
      /* JSで制御するためいったん表示する */
      visibility: visible;
      opacity: 1;
      /* JSのslidetoggleで表示させるため非表示に */
      display: none;
      /* JSで制御するためCSSのアニメーションを切る */
      transition: none;
    }
    nav ul li a {
      border-bottom: 1px solid #ccc;
    }
    /* 矢印の位置と向き */
    nav ul li.has-child::before {
      left: 20px;
    }
    nav ul ul li.has-child::before {
      transform: rotate(135deg);
      left: 20px;
    }

    nav ul li.has-child.active::before {
      transform: rotate(-45deg);
    }
  }
</style>
