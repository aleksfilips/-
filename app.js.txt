// Инициализация скриптов после загрузки контента
document.addEventListener('DOMContentLoaded', () => {
  initSmoothScrolling();
  initModal();
  initForm();
});

// Плавный скролл
function initSmoothScrolling() {
  const links = document.querySelectorAll('.nav__link');
  links.forEach(link => {
    link.addEventListener('click', e => {
      e.preventDefault();
      const id = link.getAttribute('href');
      const target = document.querySelector(id);
      if (!target) return;
      const headerHeight = document.querySelector('.header').offsetHeight;
      const offset = target.offsetTop - headerHeight - 20;
      window.scrollTo({ top: offset, behavior: 'smooth' });
    });
  });
}

// Модальное окно
function initModal() {
  const modal = document.getElementById('modal');
  const modalSuccess = document.getElementById('successModal');
  
  window.openModal = () => {
    modal.classList.add('active');
  }
  
  window.closeModal = () => {
    modal.classList.remove('active');
  }
  
  window.closeSuccessModal = () => {
    modalSuccess.classList.remove('active');
  }
  
  const overlay = document.querySelectorAll('.modal-overlay');
  overlay.forEach(el => {
    el.addEventListener('click', closeModal);
    el.addEventListener('click', closeSuccessModal);
  });
  
  document.addEventListener('keydown', e => {
    if (e.key === 'Escape') {
      closeModal();
      closeSuccessModal();
    }
  });
}

// Обработка формы
function initForm() {
  const form = document.getElementById('orderForm');
  form.addEventListener('submit', event => {
    event.preventDefault();

    // Простейшая валидация
    if (!form.name.value.trim() || !form.phone.value.trim() || !form.plan.value) {
      alert('Пожалуйста, заполните все поля.');
      return;
    }

    // Имитация отправки
    form.querySelector('button[type="submit"]').disabled = true;
    form.querySelector('button[type="submit"]').innerText = 'Отправка...';

    setTimeout(() => {
      form.reset();
      form.querySelector('button[type="submit"]').disabled = false;
      form.querySelector('button[type="submit"]').innerText = 'Оформить заказ';
      closeModal();
      document.getElementById('successModal').classList.add('active');
    }, 1500);
  });
}
