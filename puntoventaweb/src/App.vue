<template>
  <div class="min-h-screen bg-gradient-to-br from-slate-900 via-slate-800 to-slate-900 text-white">
    <header class="bg-slate-900/70 backdrop-blur border-b border-white/10">
      <div class="mx-auto flex max-w-6xl items-center justify-between px-6 py-5">
        <div>
          <p class="text-sm uppercase tracking-[0.4em] text-slate-400">Punto de Venta</p>
          <h1 class="text-2xl font-bold text-white">Impulsa tu negocio con tecnología inteligente</h1>
        </div>
        <button
          v-if="!isAuthenticated"
          class="rounded-full bg-emerald-500 px-6 py-2 text-sm font-semibold text-white shadow-lg shadow-emerald-500/30 transition hover:bg-emerald-400 focus:outline-none focus:ring-2 focus:ring-emerald-300"
          @click="openModal('login')"
        >
          Iniciar sesión
        </button>
        <p v-else class="text-sm text-emerald-300">Sesión activa</p>
      </div>
    </header>

    <main class="mx-auto max-w-6xl px-6 py-12">
      <section v-if="currentView === 'home'" class="space-y-16">
        <div class="grid gap-10 md:grid-cols-[1.1fr_0.9fr]">
          <div class="space-y-6">
            <span class="inline-flex items-center gap-2 rounded-full bg-white/10 px-4 py-1 text-xs font-semibold uppercase tracking-[0.3em] text-slate-200">
              Nuevo
            </span>
            <h2 class="text-4xl font-bold leading-tight text-white md:text-5xl">
              Descubre las funcionalidades que transformarán tu punto de venta.
            </h2>
            <p class="text-lg text-slate-300">
              Gestiona, analiza y haz crecer tu negocio con herramientas diseñadas para vendedores modernos.
            </p>
            <div class="flex flex-wrap items-center gap-4 text-sm text-slate-300">
              <div class="flex items-center gap-2 rounded-full bg-white/5 px-4 py-2">
                <span class="h-2 w-2 rounded-full bg-emerald-400"></span>
                Plataforma siempre disponible
              </div>
              <div class="flex items-center gap-2 rounded-full bg-white/5 px-4 py-2">
                <span class="h-2 w-2 rounded-full bg-blue-400"></span>
                Información en tiempo real
              </div>
            </div>
          </div>
          <div class="relative">
            <div class="absolute -left-10 top-10 hidden h-20 w-20 rounded-full border border-white/20 md:block"></div>
            <div class="absolute -right-6 bottom-8 hidden h-24 w-24 rounded-full border border-white/20 md:block"></div>
            <div class="relative overflow-hidden rounded-3xl border border-white/10 bg-white/5 p-6 shadow-xl">
              <div class="grid grid-cols-2 gap-4 text-xs text-slate-200">
                <div class="rounded-2xl bg-slate-900/70 p-4">
                  <p class="text-4xl font-bold text-emerald-300">98%</p>
                  <p class="mt-2 font-semibold">Clientes satisfechos</p>
                </div>
                <div class="rounded-2xl bg-slate-900/70 p-4">
                  <p class="text-4xl font-bold text-sky-300">24/7</p>
                  <p class="mt-2 font-semibold">Soporte dedicado</p>
                </div>
                <div class="col-span-2 rounded-2xl bg-slate-900/70 p-4">
                  <p class="text-sm text-slate-300">
                    "La plataforma más intuitiva para administrar nuestras sucursales."
                  </p>
                  <p class="mt-3 text-xs uppercase tracking-[0.3em] text-slate-500">Cafe Loop · CDMX</p>
                </div>
              </div>
            </div>
          </div>
        </div>

        <section>
          <h3 class="text-2xl font-semibold text-white">Beneficios destacados</h3>
          <p class="mt-2 max-w-3xl text-slate-300">
            Explora las herramientas creadas para potenciar cada aspecto de tu operación. Haz clic para conocer más.
          </p>
          <div class="mt-10 grid gap-6 sm:grid-cols-2 lg:grid-cols-3">
            <button
              v-for="benefit in benefits"
              :key="benefit.id"
              class="group relative overflow-hidden rounded-3xl border border-white/10 bg-white/5 p-6 text-left transition hover:-translate-y-1 hover:border-white/30 hover:bg-white/10"
              @click="openBenefitModal(benefit)"
            >
              <span class="absolute inset-0 bg-gradient-to-br from-emerald-400/0 via-white/0 to-white/5 transition group-hover:via-emerald-400/10"></span>
              <div class="relative space-y-4">
                <div class="flex h-12 w-12 items-center justify-center rounded-2xl bg-emerald-400/20 text-emerald-300">
                  <span class="text-lg font-bold">{{ benefit.icon }}</span>
                </div>
                <h4 class="text-xl font-semibold text-white">{{ benefit.title }}</h4>
                <p class="text-sm leading-relaxed text-slate-300">{{ benefit.summary }}</p>
                <span class="inline-flex items-center gap-2 text-sm font-semibold text-emerald-300">
                  Ver más
                  <svg class="h-4 w-4" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" d="m9 5 7 7-7 7"></path>
                  </svg>
                </span>
              </div>
            </button>
          </div>
        </section>
      </section>

      <section v-else-if="currentView === 'dashboard'" class="rounded-3xl border border-white/10 bg-white/5 p-10 text-center shadow-lg">
        <h2 class="text-3xl font-bold text-white">Dashboard</h2>
        <p class="mt-4 text-lg text-slate-300">¡Inicio de sesión correcto!</p>
        <div class="mt-8 rounded-2xl bg-slate-900/70 p-6 text-white">
          <p class="text-xl font-semibold">Aquí va la información importante</p>
          <p class="mt-3 text-sm text-slate-300">
            Personaliza esta sección con las métricas clave y accesos directos que tu negocio necesita.
          </p>
        </div>
      </section>
    </main>

    <transition name="fade">
      <div
        v-if="selectedBenefit"
        class="fixed inset-0 z-40 flex items-center justify-center bg-slate-900/80 px-6 py-10"
        @click.self="closeBenefitModal"
      >
        <div class="max-h-full w-full max-w-3xl overflow-y-auto rounded-3xl border border-white/10 bg-slate-900 p-8 shadow-2xl">
          <div class="flex items-start justify-between gap-6">
            <div>
              <h4 class="text-3xl font-bold text-white">{{ selectedBenefit.title }}</h4>
              <p class="mt-3 text-sm uppercase tracking-[0.4em] text-emerald-300">Funcionalidad</p>
            </div>
            <button
              class="rounded-full bg-white/10 p-2 text-slate-300 transition hover:bg-white/20"
              @click="closeBenefitModal"
            >
              <svg class="h-5 w-5" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
                <path stroke-linecap="round" stroke-linejoin="round" d="m6 18 12-12M6 6l12 12" />
              </svg>
            </button>
          </div>
          <img
            :src="selectedBenefit.image"
            :alt="selectedBenefit.title"
            class="mt-6 h-52 w-full rounded-2xl object-cover"
          />
          <p class="mt-6 text-base leading-relaxed text-slate-300">{{ selectedBenefit.description }}</p>
        </div>
      </div>
    </transition>

    <transition name="fade">
      <div
        v-if="activeModal"
        class="fixed inset-0 z-50 flex items-center justify-center bg-slate-900/90 px-6"
      >
        <div class="w-full max-w-md rounded-3xl border border-white/10 bg-slate-900 p-8 shadow-xl">
          <div class="mb-6 text-center">
            <h3 class="text-2xl font-bold text-white">{{ modalTitles[activeModal] }}</h3>
            <p class="mt-2 text-sm text-slate-400">{{ modalDescriptions[activeModal] }}</p>
          </div>

          <form v-if="activeModal === 'login'" class="space-y-5" @submit.prevent="handleLogin">
            <div>
              <label class="text-sm font-semibold text-slate-200">Correo electrónico</label>
              <input
                v-model.trim="loginForm.email"
                type="email"
                placeholder="usuario@correo.com"
                class="mt-1 w-full rounded-xl border border-white/10 bg-white/5 px-4 py-3 text-sm text-white placeholder:text-slate-500 focus:border-emerald-400 focus:outline-none"
              />
              <p v-if="loginForm.email && !emailIsValid(loginForm.email)" class="mt-1 text-xs text-rose-400">
                Ingrese un correo válido.
              </p>
            </div>
            <div>
              <label class="text-sm font-semibold text-slate-200">Contraseña</label>
              <input
                v-model.trim="loginForm.password"
                type="password"
                placeholder="********"
                class="mt-1 w-full rounded-xl border border-white/10 bg-white/5 px-4 py-3 text-sm text-white placeholder:text-slate-500 focus:border-emerald-400 focus:outline-none"
              />
              <p v-if="loginForm.password && !passwordIsValid(loginForm.password)" class="mt-1 text-xs text-rose-400">
                Debe tener mínimo 8 caracteres, mayúscula, minúscula, número y símbolo.
              </p>
            </div>
            <button
              type="submit"
              class="w-full rounded-full bg-emerald-500 px-4 py-3 text-sm font-semibold text-white shadow-lg shadow-emerald-500/30 transition hover:bg-emerald-400 disabled:cursor-not-allowed disabled:bg-slate-600 disabled:shadow-none"
              :disabled="!loginIsValid"
            >
              Iniciar sesión
            </button>
            <p v-if="loginMessage" class="text-center text-sm text-emerald-300">{{ loginMessage }}</p>
            <div class="flex flex-col items-center gap-2 text-sm text-slate-300">
              <button type="button" class="font-semibold text-emerald-300 hover:underline" @click="switchModal('register')">
                Registrarse
              </button>
              <button type="button" class="hover:underline" @click="switchModal('recover')">
                ¡Olvidaste tu contraseña?
              </button>
            </div>
          </form>

          <form v-else-if="activeModal === 'register'" class="space-y-5" @submit.prevent="handleRegister">
            <div>
              <label class="text-sm font-semibold text-slate-200">Nombre completo</label>
              <input
                v-model.trim="registerForm.name"
                type="text"
                placeholder="Nombre y apellidos"
                class="mt-1 w-full rounded-xl border border-white/10 bg-white/5 px-4 py-3 text-sm text-white placeholder:text-slate-500 focus:border-sky-400 focus:outline-none"
              />
            </div>
            <div>
              <label class="text-sm font-semibold text-slate-200">Correo electrónico</label>
              <input
                v-model.trim="registerForm.email"
                type="email"
                placeholder="usuario@correo.com"
                class="mt-1 w-full rounded-xl border border-white/10 bg-white/5 px-4 py-3 text-sm text-white placeholder:text-slate-500 focus:border-sky-400 focus:outline-none"
              />
              <p v-if="registerForm.email && !emailIsValid(registerForm.email)" class="mt-1 text-xs text-rose-400">
                Ingrese un correo válido.
              </p>
            </div>
            <div>
              <label class="text-sm font-semibold text-slate-200">Contraseña</label>
              <input
                v-model.trim="registerForm.password"
                type="password"
                placeholder="********"
                class="mt-1 w-full rounded-xl border border-white/10 bg-white/5 px-4 py-3 text-sm text-white placeholder:text-slate-500 focus:border-sky-400 focus:outline-none"
              />
              <p v-if="registerForm.password && !passwordIsValid(registerForm.password)" class="mt-1 text-xs text-rose-400">
                Debe tener mínimo 8 caracteres, mayúscula, minúscula, número y símbolo.
              </p>
            </div>
            <div>
              <label class="text-sm font-semibold text-slate-200">Confirmar contraseña</label>
              <input
                v-model.trim="registerForm.confirmPassword"
                type="password"
                placeholder="********"
                class="mt-1 w-full rounded-xl border border-white/10 bg-white/5 px-4 py-3 text-sm text-white placeholder:text-slate-500 focus:border-sky-400 focus:outline-none"
              />
              <p
                v-if="registerForm.confirmPassword && registerForm.confirmPassword !== registerForm.password"
                class="mt-1 text-xs text-rose-400"
              >
                Las contraseñas deben coincidir.
              </p>
            </div>
            <button
              type="submit"
              class="w-full rounded-full bg-sky-500 px-4 py-3 text-sm font-semibold text-white shadow-lg shadow-sky-500/30 transition hover:bg-sky-400 disabled:cursor-not-allowed disabled:bg-slate-600 disabled:shadow-none"
              :disabled="!registerIsValid"
            >
              Guardar
            </button>
            <p v-if="registerMessage" class="text-center text-sm text-emerald-300">{{ registerMessage }}</p>
            <div class="flex justify-center">
              <button type="button" class="text-sm text-slate-300 hover:underline" @click="switchModal('login')">
                ¿Ya tienes cuenta? Inicia sesión
              </button>
            </div>
          </form>

          <form v-else-if="activeModal === 'recover'" class="space-y-5" @submit.prevent="handleRecover">
            <div>
              <label class="text-sm font-semibold text-slate-200">Correo electrónico</label>
              <input
                v-model.trim="recoverForm.email"
                type="email"
                placeholder="usuario@correo.com"
                class="mt-1 w-full rounded-xl border border-white/10 bg-white/5 px-4 py-3 text-sm text-white placeholder:text-slate-500 focus:border-violet-400 focus:outline-none"
              />
              <p v-if="recoverForm.email && !emailIsValid(recoverForm.email)" class="mt-1 text-xs text-rose-400">
                Ingrese un correo válido.
              </p>
            </div>
            <button
              type="submit"
              class="w-full rounded-full bg-violet-500 px-4 py-3 text-sm font-semibold text-white shadow-lg shadow-violet-500/30 transition hover:bg-violet-400 disabled:cursor-not-allowed disabled:bg-slate-600 disabled:shadow-none"
              :disabled="!recoverIsValid"
            >
              Recuperar contraseña
            </button>
            <p v-if="recoverMessage" class="text-center text-sm text-emerald-300">{{ recoverMessage }}</p>
            <div class="flex justify-center">
              <button type="button" class="text-sm text-slate-300 hover:underline" @click="switchModal('login')">
                Volver a iniciar sesión
              </button>
            </div>
          </form>
        </div>
      </div>
    </transition>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent, reactive, ref } from 'vue';

type Benefit = {
  id: number;
  title: string;
  summary: string;
  description: string;
  image: string;
  icon: string;
};

type ModalType = 'login' | 'register' | 'recover';

const emailRegex = /^[\w-.]+@([\w-]+\.)+[\w-]{2,}$/i;
const passwordRegex = /^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[^A-Za-z0-9]).{8,}$/;

export default defineComponent({
  name: 'App',
  setup() {
    const currentView = ref<'home' | 'dashboard'>('home');
    const isAuthenticated = ref(false);

    const benefits = ref<Benefit[]>([
      {
        id: 1,
        title: 'Inventario Inteligente',
        summary: 'Controla existencias en tiempo real y evita quiebres o exceso de stock.',
        description:
          'Monitorea cada producto desde la recepción hasta la venta con alertas inteligentes de existencias bajas, sugerencias de reorden y reportes automáticos para optimizar tus compras.',
        image: 'https://images.unsplash.com/photo-1582407947304-fd86f028f716?auto=format&fit=crop&w=1200&q=80',
        icon: 'IN'
      },
      {
        id: 2,
        title: 'Reportes Dinámicos',
        summary: 'Visualiza indicadores clave con dashboards personalizables.',
        description:
          'Crea tableros con métricas esenciales como ventas diarias, ticket promedio, artículos más vendidos y rendimiento por sucursal. Exporta fácilmente a PDF o Excel para tus reuniones.',
        image: 'https://images.unsplash.com/photo-1551288049-bebda4e38f71?auto=format&fit=crop&w=1200&q=80',
        icon: 'RD'
      },
      {
        id: 3,
        title: 'Ventas Omnicanal',
        summary: 'Integra tu tienda física y online en una misma experiencia.',
        description:
          'Sincroniza catálogos, precios y promociones en todos tus canales. Ofrece retiro en tienda, entregas rápidas y seguimiento de pedidos desde una única plataforma.',
        image: 'https://images.unsplash.com/photo-1483478550801-ceba5fe50e8e?auto=format&fit=crop&w=1200&q=80',
        icon: 'VO'
      },
      {
        id: 4,
        title: 'Caja Rápida',
        summary: 'Procesa cobros en segundos con múltiples métodos de pago.',
        description:
          'Registra ventas con lector de códigos, pagos con tarjeta, efectivo o billeteras digitales. Genera facturas instantáneas y envíalas por correo a tus clientes.',
        image: 'https://images.unsplash.com/photo-1563013544-824ae1b704d3?auto=format&fit=crop&w=1200&q=80',
        icon: 'CR'
      },
      {
        id: 5,
        title: 'Fidelización de Clientes',
        summary: 'Diseña programas de puntos y recompensas irresistibles.',
        description:
          'Crea segmentos personalizados, envía promociones automáticas y mide la recurrencia de tus clientes para aumentar la lealtad y el valor de cada ticket.',
        image: 'https://images.unsplash.com/photo-1521737604893-d14cc237f11d?auto=format&fit=crop&w=1200&q=80',
        icon: 'FC'
      },
      {
        id: 6,
        title: 'Gestión de Empleados',
        summary: 'Controla permisos, roles y desempeño por colaborador.',
        description:
          'Asigna roles personalizados, registra horarios, mide ventas individuales y establece objetivos claros para tu equipo con reportes fáciles de interpretar.',
        image: 'https://images.unsplash.com/photo-1521737604893-d14cc237f11d?auto=format&fit=crop&w=1200&q=80',
        icon: 'GE'
      },
      {
        id: 7,
        title: 'Alertas Inteligentes',
        summary: 'Recibe notificaciones proactivas sobre eventos críticos.',
        description:
          'Detecta diferencias de caja, productos por caducar o ventas inusuales. Configura alertas por correo, SMS o notificaciones push para actuar a tiempo.',
        image: 'https://images.unsplash.com/photo-1504384308090-c894fdcc538d?auto=format&fit=crop&w=1200&q=80',
        icon: 'AI'
      },
      {
        id: 8,
        title: 'Integración Contable',
        summary: 'Sincroniza tus movimientos con el sistema contable.',
        description:
          'Genera pólizas automáticas, clasifica gastos e ingresos y concilia movimientos con tu contabilidad sin tareas repetitivas.',
        image: 'https://images.unsplash.com/photo-1454165205744-3b78555e5572?auto=format&fit=crop&w=1200&q=80',
        icon: 'IC'
      },
      {
        id: 9,
        title: 'Compras Automatizadas',
        summary: 'Planifica órdenes con base en demanda y temporadas.',
        description:
          'Automatiza pedidos con proveedores preferidos, controla costos y recibe sugerencias basadas en históricos y tendencias del mercado.',
        image: 'https://images.unsplash.com/photo-1460925895917-afdab827c52f?auto=format&fit=crop&w=1200&q=80',
        icon: 'CA'
      },
      {
        id: 10,
        title: 'Análisis de Clientes',
        summary: 'Identifica hábitos de consumo y preferencias en segundos.',
        description:
          'Cruza información demográfica con el historial de compras para diseñar campañas personalizadas y ofertas relevantes en cada momento.',
        image: 'https://images.unsplash.com/photo-1521737604893-d14cc237f11d?auto=format&fit=crop&w=1200&q=80',
        icon: 'AC'
      }
    ]);

    const selectedBenefit = ref<Benefit | null>(null);
    const activeModal = ref<ModalType | null>(null);

    const loginForm = reactive({
      email: '',
      password: ''
    });
    const registerForm = reactive({
      name: '',
      email: '',
      password: '',
      confirmPassword: ''
    });
    const recoverForm = reactive({
      email: ''
    });

    const loginMessage = ref('');
    const registerMessage = ref('');
    const recoverMessage = ref('');

    const emailIsValid = (value: string) => emailRegex.test(value);
    const passwordIsValid = (value: string) => passwordRegex.test(value);

    const loginIsValid = computed(() => emailIsValid(loginForm.email) && passwordIsValid(loginForm.password));
    const registerIsValid = computed(
      () =>
        registerForm.name.trim().length > 0 &&
        emailIsValid(registerForm.email) &&
        passwordIsValid(registerForm.password) &&
        registerForm.password === registerForm.confirmPassword
    );
    const recoverIsValid = computed(() => emailIsValid(recoverForm.email));

    const modalTitles: Record<ModalType, string> = {
      login: 'Iniciar sesión',
      register: 'Crear una cuenta',
      recover: 'Recuperar contraseña'
    };

    const modalDescriptions: Record<ModalType, string> = {
      login: 'Accede a tu panel de control y lleva tu punto de venta al siguiente nivel.',
      register: 'Completa la información para comenzar a utilizar la plataforma.',
      recover: 'Ingresa el correo asociado a tu cuenta para recibir un enlace de recuperación.'
    };

    const openBenefitModal = (benefit: Benefit) => {
      selectedBenefit.value = benefit;
    };

    const closeBenefitModal = () => {
      selectedBenefit.value = null;
    };

    const openModal = (type: ModalType) => {
      activeModal.value = type;
      loginMessage.value = '';
      registerMessage.value = '';
      recoverMessage.value = '';
    };

    const switchModal = (type: ModalType) => {
      openModal(type);
    };

    const closeModal = () => {
      activeModal.value = null;
    };

    const resetForms = () => {
      loginForm.email = '';
      loginForm.password = '';
      registerForm.name = '';
      registerForm.email = '';
      registerForm.password = '';
      registerForm.confirmPassword = '';
      recoverForm.email = '';
    };

    const handleLogin = () => {
      if (!loginIsValid.value) return;
      loginMessage.value = 'Inicio de sesión correcto';
      setTimeout(() => {
        closeModal();
        currentView.value = 'dashboard';
        isAuthenticated.value = true;
        resetForms();
      }, 900);
    };

    const handleRegister = () => {
      if (!registerIsValid.value) return;
      registerMessage.value = 'Registro correcto';
      setTimeout(() => {
        closeModal();
        resetForms();
      }, 1000);
    };

    const handleRecover = () => {
      if (!recoverIsValid.value) return;
      recoverMessage.value = 'Correo enviado';
      setTimeout(() => {
        closeModal();
        resetForms();
      }, 1000);
    };

    return {
      activeModal,
      benefits,
      closeBenefitModal,
      currentView,
      emailIsValid,
      handleLogin,
      handleRecover,
      handleRegister,
      isAuthenticated,
      loginForm,
      loginIsValid,
      loginMessage,
      modalDescriptions,
      modalTitles,
      openBenefitModal,
      openModal,
      passwordIsValid,
      recoverForm,
      recoverIsValid,
      recoverMessage,
      registerForm,
      registerIsValid,
      registerMessage,
      selectedBenefit,
      switchModal
    };
  }
});
</script>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.25s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
