<template>
  <header>
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
  </header>
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

<style scoped></style>
