<template>
  <header>
    <p>Bárbara Vilardi</p>

    <nav>
      <ul>
        <li><a href="#home">Início</a></li>
        <li><a href="#services">Serviços</a></li>
        <li><a href="#about">Sobre mim</a></li>
        <li><a href="#contact">Contato</a></li>
      </ul>
    </nav>
  </header>
</template>

<script></script>

<style lang="scss" scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem;
  background: #f0fdf4;
  position: fixed;
  width: 100%;
  top: 0;
  z-index: 1000;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
  transition: all 0.3s ease;

  nav {
    ul {
      list-style: none;
      display: flex;
      gap: 20px;

      li {
        a {
          color: #2d3748;
          text-decoration: none;
          font-weight: 500;
          position: relative;
          transition: color 0.3s ease;
        }

        a::after {
          content: '';
          position: absolute;
          bottom: -5px;
          left: 0;
          width: 0;
          height: 2px;
          background: #10b981;
          transition: width 0.3s ease;
        }

        a:hover {
          color: #10b981;
        }

        a:hover::after {
          width: 100%;
        }
      }
    }
  }
}
</style>
