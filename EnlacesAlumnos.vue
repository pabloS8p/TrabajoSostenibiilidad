<template>
  <div class="contenedor">
    <h2>🌱Proyectos de Alumnos</h2>
    <div class="tarjetas">
      <div
        v-for="(item, index) in trabajos"
        :key="index"
        class="tarjeta"
        @mouseenter="hoverIndex = index"
        @mouseleave="hoverIndex = null"
        :class="{ 'tarjeta-hover': hoverIndex === index }">
        <h3>{{ item.titulo }}</h3>
        <p><strong>Autores:</strong> {{ item.autores.join(", ") }}</p>
        <a
          :href="item.enlace"
          target="_blank"
          rel="noopener"
          class="btn-85"
        >
          <span>Ver Proyecto</span>
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";

export default {
  name: "TrabajosAlumnos",
  setup() {
    const hoverIndex = ref(null);

    const trabajos = ref([
      {
        titulo: "titulo",
        autores: ["alumnos"],
        enlace: "https://example.com/huerto-escolar",
      },
      {
        titulo: "titulo",
        autores: ["alumnos"],
        enlace: "https://example.com/energia-verde",
      },
      {
        titulo: "titulo",
        autores: ["alumnos"],
        enlace: "https://example.com/reciclaje-automatizado",
      },
    ]);

    return {
      trabajos,
      hoverIndex,
    };
  },
};
</script>

<style scoped>
.contenedor {
  padding-top: 0.5rem;
  padding-right: 2rem;
  padding-bottom: 2rem;
  padding-left: 2rem;
  max-width: 900px;
  margin: 0 auto;
  position: relative;
}

h2 {
  margin-bottom: 1.5rem;
  color: #42b883;
  text-align: center;
}

.tarjetas {
  display: grid;
  gap: 3rem;
  grid-template-columns: repeat(3, 1fr);
}

.tarjeta {
  background-color: #303030;
  border-left: 6px solid #42b883;
  padding: 1.5rem;
  border-radius: 12px;
  box-shadow: 0 6px 10px rgb(0 0 0 / 0.1);
  transform-origin: center;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  min-height: 250px;
}

.tarjeta-hover {
  transform: scale(1.20);
  box-shadow: 0 10px 20px rgb(0 0 0 / 0.2);
}

h3 {
  margin-bottom: 0.4rem;
  color: #1b4332;
}

p {
  margin-bottom: 1rem;
  color: #42b883;
  font-weight: 600;
}

/* Botón animado */
.btn-85,
.btn-85 *,
.btn-85 :after,
.btn-85 :before,
.btn-85:after,
.btn-85:before {
  border: 0 solid;
  box-sizing: border-box;
}
.btn-85 {
  -webkit-tap-highlight-color: transparent;
  -webkit-appearance: button;
  appearance: button;
  background-color: #000;
  background-image: none;
  color: #42b883;
  cursor: pointer;
  font-family: ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont,
    Segoe UI, Roboto, Helvetica Neue, Arial, Noto Sans, sans-serif,
    Apple Color Emoji, Segoe UI Emoji, Segoe UI Symbol, Noto Color Emoji;
  font-size: 100%;
  font-weight: 900;
  line-height: 1.5;
  margin: 0;
  -webkit-mask-image: -webkit-radial-gradient(#000, #ffffff);
  mask-image: radial-gradient(#000, #ffffff);
  padding: 1.2rem 3rem;
  border-radius: 999px;
  display: block;
  position: relative;
  text-transform: uppercase;
  transition: background-color 0.3s ease;
}
.btn-85 span {
  font-weight: 100;
  mix-blend-mode: difference;
  transition: opacity 0.2s;
}
.btn-85:hover span {
  animation: text-reset 0.2s 0.8s forwards;
  opacity: 0;
}
.btn-85:after,
.btn-85:before {
  border: 4px solid #42b883;
  border-radius: 999px;
  content: "";
  height: 100%;
  left: 0;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  transition: height 0.2s cubic-bezier(0.41, 2.01, 0.64, 1);
  width: 100%;
}
.btn-85:after {
  background: #315b4a;
  border: none;
  height: 2rem;
  width: 0;
  z-index: -1;
}
.btn-85:hover:before {
  animation: border-reset 0.2s cubic-bezier(0.41, 2.01, 0.64, 1) 0.78s forwards;
  height: 2rem;
}
.btn-85:hover:after {
  animation: progress-bar 1s cubic-bezier(0.41, 2.01, 0.64, 1) forwards;
}
@keyframes progress-bar {
  0% {
    opacity: 1;
    width: 0;
  }
  10% {
    opacity: 1;
    width: 15%;
  }
  25% {
    opacity: 1;
    width: 25%;
  }
  40% {
    opacity: 1;
    width: 35%;
  }
  55% {
    opacity: 1;
    width: 75%;
  }
  60% {
    opacity: 1;
    width: 100%;
  }
  to {
    opacity: 0;
    width: 100%;
  }
}
@keyframes border-reset {
  0% {
    height: 2rem !important;
  }
  to {
    height: 100% !important;
  }
}
@keyframes text-reset {
  0% {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
</style>