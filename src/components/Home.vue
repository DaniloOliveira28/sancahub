<template>
  <section>
    <div class="Alert" :class="alertStyle">
      <p class="Alert__title">
         <b>Associação de Empresas de Tecnologia do Sancahub.</b>
         <br>
         <span>Nosso propósito é transformar São Carlos no mais relevante ecossistema de tecnologia e de inovação da América Latina</span>
         <br><br>

         <b>Sua empresa quer participar do nosso movimento?</b>
         <br>
         <span>Nos mande um email: contato@sancahub.org</span>
      </p>
    </div>
    <div class="CompanieList">
      <div
        v-for="companie in companies"
        class="CompanieList__item"
        @click="openModal(companie)"
      >
        <div class="CompanieList__imageBox">
          <img class="CompanieList__image" :src="`static/companies/images/${companie.logo}`" :alt="companie.name">
        </div>
        <div class="CompanieList__info">
          <span class="CompanieList__name">{{ companie.name }}</span>
          <span class="CompanieList__description">{{ companie.description || 'Descrição' }}</span>
        </div>
      </div>
    </div>
    <modal
      v-if="isModalOpen"
      @close="closeModal"
    >
      <div slot="content" class="container">
        <div class="Companie">
          <div class="Companie__image">
            <a :href="companie.href" target="_blank">
              <img :src="`static/companies/images/${companie.logo}`" :alt="companie.name">
            </a>
          </div>
          <a class="Companie__name" :href="companie.href" target="_blank">
            {{ companie.name }}
          </a>
          <div class="Companie__description">{{ companie.description || ' ' }}</div>
        </div>
      </div>
    </modal>
  </section>
</template>

<script>
  import Modal from './Modal';
  import Companies from '../../static/companies/companies.json';
  export default {
    name: 'home',
    data() {
      return {
        companies: [],
        isModalOpen: false,
        isEditalVisible: false,
        companie: {},
      };
    },
    created() {
      this.companies = this.shuffleArray(Companies.companies);
//      axios.get('/static/companies/companies.json')
//        .then(({ data }) => {
//          this.companies = this.shuffleArray(data.companies);
//        });
    },
    methods: {
      openModal(companie) {
        this.companie = companie;
        this.isModalOpen = true;
      },
      closeModal() {
        this.isModalOpen = false;
      },
      shuffleArray(array) {
        for (let i = array.length - 1; i > 0; i--) {
          let j = Math.floor(Math.random() * (i + 1));
          let temp = array[i];
          array[i] = array[j];
          array[j] = temp;
        }
        return array;
      },
    },
    computed: {
      alertStyle() {
        return {
          'is-open': this.isEditalVisible,
        };
      },
    },
    components: {
      Modal,
    },
  };
</script>


<style>
  .Alert {
    padding: 1rem;
    background: #169a3e;
    color: #fff;
    font-weight: 500;
    font-weight: 300;
  }
  .Alert .container {
    text-align: justify;
  }
  .Alert__title {
    font-weight: 500;
    line-height: 1.6;
  }
  .Alert strong {
    font-weight: 500;
  }
  .CompanieList {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    padding-top: 24px;
  }

  .CompanieList__item {
    transition: all 0.3s;
    will-change: transform;
    text-decoration: none;
    margin: 6px;
    cursor: pointer;
  }
  .CompanieList__item:hover {
    /*transform: scale(1.1);*/
    box-shadow: 0 12px 48px rgba(0, 0, 0, 0.1);
    z-index: 2;
  }
  .CompanieList__imageBox {
    width: 300px;
    height: 300px;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    background: #fff;
    user-select: none;
  }
  .CompanieList__info {
    background: #ffffff;
    padding: 1rem;
    color: #333;
    border-top: 1px solid #f1f1f1;
    max-width: 300px;
  }
  .CompanieList__name,
  .CompanieList__description {
    display: block;
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
  }
  .CompanieList__name {
    font-weight: 600;
  }
  .CompanieList__description {
    font-weight: 300;
    margin-top: 6px;
    color: #666;
  }
  .CompanieList__image {
    max-width: 200px;
    max-height: 140px;
  }

  /*Modal*/
  .Companie {
    text-align: center;
  }
  .Companie__image img {
    max-height: 180px;
  }
  .Companie__image {
    max-width: 240px;
    width: 100%;
    display: block;
    margin: 0 auto;
  }
  .Companie__name {
    font-weight: 800;
    font-size: 1.8rem;
    margin-top: 2rem;
    color: #333;
    display: inline-block;
  }
  .Companie__description {
    margin-top: 2rem;
    font-size: 1rem;
    font-weight: 300;
    line-height: 1.45;
  }
  .Link__icon {
    display: inline;
    width: 24px;
    height: 24px;
    fill: rgba(0, 0, 0, 0.6);
    margin-top: -10px;
    margin-left: 6px;
  }
  .Alert.is-open > .Alert__icon {
    transform: rotate(180deg)translateY(10px);
  }
  .Alert__icon {
    width: 48px;
    height: 48px;
    cursor: pointer;
    fill: rgba(255, 255, 255, 1);
  }
  @media screen and (min-width: 768px) {
    .Companie__name {
      font-size: 2.4rem;
    }
    .Companie__description {
      font-size: 1.4rem;
    }
  }
</style>
