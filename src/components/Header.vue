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

<script setup></script>

<style scoped></style>
