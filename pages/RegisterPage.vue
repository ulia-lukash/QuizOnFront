<template>
  <div class="main">
    <div class="form center">

        <div v-if="showAlert">
            <alert-vue @dismissAlert="showAlert=false" :alertText=this.alertText :alertHeader=this.alertHeader />
        </div>

                <div class = "header center">
                    РЕГИСТРАЦИЯ НА ИГРУ
                </div>

                <div class = "game_num center">
                    2-я игра Бауманской лиги
                </div>

                <div class = "info center">
                    <div class = "info_clock"><img src = "../assets/images/clock.svg" ></div>
                    <div class = "info_text">24 октября, ВТ 19:00</div>
                </div>

                <div class = "info center">
                    <div class = "info_loc"><img src = "../assets/images/location.svg"></div>
                    <div class = "info_text">345 аудитория (ГУК МГТУ им. Н.Э. Баумана)</div>
                </div>


                <form class = "btn_container center">
                    <div class = "block_input center">
                        <div class = "block_text">
                            ИМЯ КАПИТАНА <span class="star">*</span>
                        </div>
                        <input v-model="form.captain_name" :class="{ error: formFormatters.captainNameIsEmpty }" required class = "input" type = "text" placeholder = "Николай Эрнестович Бауман">
                    </div>
                    <div class = "block_input center">
                        <div class = "block_text">
                            УЧЕБНАЯ ГРУППА КАПИТАНА <span class="star">*</span>
                        </div>
                        <input v-model="form.group_name" :class="{ error: formFormatters.groupNameIsEmpty }"   required class = "input" type = "text" placeholder = "СМ1-11">
                    </div>

                    <div class = "block_input center">
                        <div class = "block_text">
                            НОМЕР ТЕЛЕФОНА <span class="star">*</span>
                        </div>
                        <input v-model="form.phone" :class="{ error: formFormatters.phoneIsEmpty }"  required class = "input" type = "text"  placeholder = "8(999)888-77-66">
                    </div>
                    <div class = "block_input center">
                        <div class = "block_text">
                            ТЕЛЕГРАМ <span class="star">*</span>
                        </div>
                        <input v-model="form.tg_contact" :class="{ error: formFormatters.tgContactIsEmpty }"  required class = "input" type = "text" placeholder = "@username">
                    </div>
                    <div class = "block_input center">
                        <div class = "block_text">
                            НАЗВАНИЕ КОМАНДЫ <span class="star">*</span>
                        </div>
                        <input v-model="form.team_name" :class="{ error: formFormatters.teamNameIsEmpty }"  required class = "input" type = "text" placeholder = "Ураган Донам">
                    </div>
                    <div class = "block_input center">
                        <div class = "block_text">
                            КОЛИЧЕСТВО ЧЕЛОВЕК <span class="star">*</span>
                        </div>
                        <input v-model="form.amount" :class="{ error: formFormatters.teamSizeIsEmpty }"  required class = "input" type = "text" placeholder = "6">
                    </div>
                    <div class = "block_input center">
                        <div class = "block_text">
                            ID КОМАНДЫ
                        </div>
                        <input v-model="this.form.team_id" required class = "input" type = "text" placeholder = 0002>
                    </div>

                    <button type="button" class = "reg_btn" v-on:click="buttonClicked" >Зарегистрироваться</button>

                    <div class="agreement">
                        Отправляя свои данные, вы соглашаетесь на 
                        <NuxtLink to="/userAgreement"  href="" class="agreement_link"> обработку персональных данных</NuxtLink>
                    </div>
                </form>

            </div>
  </div>
</template>

<script>
import AlertVue from '../components/AlertVue.vue';

export default {
    name: 'RegisterPage',
    components: { AlertVue },
    data() {
      return {
        formFormatters: {
            captainNameIsEmpty: false,
            groupNameIsEmpty: false,
            phoneIsEmpty: false,
            teamNameIsEmpty: false,
            teamSizeIsEmpty: false,
            tgContactIsEmpty: false,
        },
        showAlert: false,
        alertText: "",
        alertHeader: "",
        form: {
            tg_contact: "",
            team_id: null, 
            captain_name: "",
            group_name: "",
            phone: "",
            team_name: "",
            amount: null,
        },
      };
    },
    methods: {
        
        buttonClicked() {
            
            
            if (this.form.captain_name === '') {
                this.formFormatters.captainNameIsEmpty = true
            } else {
                this.formFormatters.captainNameIsEmpty = false
            }
            if (this.form.group_name === '') {
                this.formFormatters.groupNameIsEmpty = true
            } else {
                this.formFormatters.groupNameIsEmpty = false
            }
            if (this.form.phone === '') {
                this.formFormatters.phoneIsEmpty = true
            } else {
                this.formFormatters.phoneIsEmpty = false
            }
            if (this.form.team_name === '') {
                this.formFormatters.teamNameIsEmpty = true
            } else {
                this.formFormatters.teamNameIsEmpty = false
            }
            if (this.form.tg_contact ==='') {
                this.formFormatters.tgContactIsEmpty = true
            } else {
                this.formFormatters.tgContactIsEmpty = false
            }
            if (this.form.amount == null || this.form.amount <= 1 ) {
                this.formFormatters.teamSizeIsEmpty = true
            } else {
                this.formFormatters.teamSizeIsEmpty = false
            }

            if (this.formFormatters.captainNameIsEmpty === false &&
            this.formFormatters.groupNameIsEmpty === false && this.formFormatters.phoneIsEmpty === false && this.formFormatters.teamNameIsEmpty === false && this.formFormatters.teamSizeIsEmpty === false && this.formFormatters.tgContactIsEmpty === false) {
                this.postData("https://www.quiz-on.ru/api/register", this.form).then((response) => {
                if (response.status !== 200) {
                    this.showAlert = true;
                    this.alertHeader = "Ошибка!"
                    this.alertText = "КОД ОТВЕТА НЕ 200"
                } else {
                    this.showAlert = true;
                    this.alertHeader = "Поздравляем!"
                    this.alertText = "ВЫ УСПЕШНО ЗАРЕГИСТРИРОВАНЫ"
                    this.form = {
                    tg_contact: "",
                    team_id: null,
                    captain_name: "",
                    group_name: "",
                    phone: "",
                    team_name: "",
                    amount: null,
            }
                }
            });
            
            } else {
                this.showAlert = true
                this.alertHeader = 'Пожалуйста'
                this.alertText = "ЗАПОЛНИТЕ ВСЕ ПОЛЯ ФОРМЫ"
            }
            
            },
            async postData(url, data) {
                try {
                    const response = await fetch(url, {
                        method: "POST",
                        mode: "cors",
                        cache: "no-cache",
                        credentials: "same-origin",
                        headers: {
                        "Content-Type": "application/json",
                        },
                        redirect: "follow",
                        referrerPolicy: "no-referrer",
                        body: JSON.stringify(data),
                    });

                    return response;
                } catch (error) {
                    this.showAlert = true;
                    this.alertHeader = "Ошибка!"
                    this.alertText = "ЧТО-ТО ПОШЛО НЕ ТАК"
                }
                
            },
    }
    
}

</script>

<style scoped>
.star {
    color: #F4DA6A;
}
.main {
    max-width: 450px;
    margin-top: 30px;
}
.form {
    width: 90vw;
    max-width: 405px;
    background-color: #1F354B;
    border-radius: 21px;
    margin: auto;
}

.center {
    margin: auto;
}

.header {
    padding-top: 17px;
    box-sizing: border-box;
    font-size: 24px;
    font-family: ProductSans;
    font-weight: 700;
    color: white;
    width: 80vw;
    max-width: 360px;
}

.game_num {
    padding-top: 17px;
    box-sizing: border-box;
    font-size: 21px;
    font-family: ProductSans;
    font-weight: 700;
    color: #F4DA6A;
    width: fit-content;
    width: 80vw;
    max-width: 360px;
}

.block_input {
    margin-top: 11px;
    width: 80vw;
    max-width: 360px;
    height: 51px;
}
.reg_btn {
    margin-top: 12px;
    background-color: #182A3E;
    border: 1.33428px solid #F4DA6A;
    border-radius: 17.3457px;
    width: 80vw;
    max-width: 360px;
    height: 35px;
    font-family: ProductSans;
    font-weight: 700;
    font-size: 17px;
    color: #FFFFFF;
}

.btn_container {
    width: 80vw;
    max-width: 360px;
    font-size: 12px;
    padding-bottom: 30px;
}

.error_output {
    margin-top: 12px;
    width: 80vw;
    max-width: 360px;
    font-family: ProductSans;
    font-weight: 400;
    overflow-wrap: break-word;
    color: #9F2128;
}

.block_text {
    font-size: 13px;
    line-height: 15px;
    font-family: ProductSans;
    font-weight: 700;
    color: #FFFFFF;
}

::placeholder {
    font-family: ProductSans;
    font-weight: 400;
    font-size: 12px;
    color: #FFFFFF33;
}

.input {
    padding: 8px;
    margin-top: 6px;
    box-sizing: border-box;
    width: 100%;
    max-width: 360px;
    height: 32px;
    border-radius: 12px;
    border-width: 2px;
    background-color: #182A3E;
    border-color: #FFFFFF33;
    color: #FFFFFF;
}

.info {
    display: flex;
    margin-top: 11px;
    width: 80vw;
    max-width: 360px;
}

.info_clock {
    max-width: 5vw;
    /* max-height: 18px; */
}

.info_loc {
    max-width: 16px;
    max-height: 21px;
}

.info_text {
    color: white;
    font-family: ProductSans;
    font-weight: 400;
    font-size: 12px;
    margin-left: 8px;
    margin-top: auto;
    margin-bottom: auto;
}
.agreement {
    margin-top: 20px;
    font-family: ProductSans;
    font-weight: 400;
    font-size: 12px;
    color: white;
}

a {
    color:#F4DA6A;
    text-decoration: none;
}

.error{
    border-color: #9F2128;
}

</style>