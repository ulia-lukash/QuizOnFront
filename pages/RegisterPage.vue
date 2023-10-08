<template>
  <div class="main">
    <div class="form center">
        <div v-if="showAlert">
            <alert-vue @dismissAlert="showAlert=false" :alertText=this.alertText :alertHeader=this.alertHeader  />
        </div>
                <div class = "header center">
                    РЕГИСТРАЦИЯ НА ИГРУ
                </div>

                <div class = "game_num center">
                    КВИЗОН №1
                </div>

                <div class = "info center">
                    <div class = "info_clock"><img src = "../assets/images/clock.svg" ></div>
                    <div class = "info_text">6 июня, ВС 20:00</div>
                </div>

                <div class = "info center">
                    <div class = "info_loc"><img src = "../assets/images/location.svg"></div>
                    <div class = "info_text">345 аудитория</div>
                </div>


                <form class = "btn_container center">
                    <div class = "block_input center">
                        <div class = "block_text">
                            ИМЯ КАПИТАНА
                        </div>
                        <input v-model="form.captain_name" :class="{ error: formFormatters.captainNameIsEmpty }" required class = "input" type = "text" placeholder = "Вася Пупкин">
                    </div>
                    <div class = "block_input center">
                        <div class = "block_text">
                            УЧЕБНАЯ ГРУППА КАПИТАНА
                        </div>
                        <input v-model="form.group" :class="{ error: formFormatters.groupIsEmpty }"   required class = "input" type = "text" placeholder = "РК6-32М">
                    </div>

                    <div class = "block_input center">
                        <div class = "block_text">
                            НОМЕР ТЕЛЕФОНА
                        </div>
                        <input v-model="form.phone" :class="{ error: formFormatters.phoneIsEmpty }"  required class = "input" type = "text"  placeholder = "88005553535">
                    </div>

                    <div class = "block_input center">
                        <div class = "block_text">
                            НАЗВАНИЕ КОМАНДЫ
                        </div>
                        <input v-model="form.team_name" :class="{ error: formFormatters.teamNameIsEmpty }"  required class = "input" type = "text" placeholder = "Ураган Донам">
                    </div>
                    <div class = "block_input center">
                        <div class = "block_text">
                            КОЛИЧЕСТВО ЧЕЛОВЕК
                        </div>
                        <input v-model="form.team_size" :class="{ error: formFormatters.teamSizeIsEmpty }"  required class = "input" type = "number" placeholder = 6>
                    </div>

                    <div class = "error_output center">
                    </div>

                    <button v-on:click="buttonClicked" type="button" class = "reg_btn">Зарегистрироваться</button>

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
  components: { AlertVue },
    name: 'RegisterPage',
    data() {
      return {
        formFormatters: {
            captainNameIsEmpty: false,
            groupIsEmpty: false,
            phoneIsEmpty: false,
            teamNameIsEmpty: false,
            teamSizeIsEmpty: false,
        },
        showAlert: false,
        alertText: "",
        alertHeader: "",
        form: {
            // userId: userId,
          captain_name: "",
          group: "",
          phone: "",
          team_name: "",
          team_size: null,
        },
      };
    },
    methods: {
        
        buttonClicked() {

            if (this.form.captain_name == '') {
                this.formFormatters.captainNameIsEmpty = true
            } else {
                this.formFormatters.captainNameIsEmpty = false
            }
            if (this.form.group == '') {
                this.formFormatters.groupIsEmpty = true
            } else {
                this.formFormatters.groupIsEmpty = false
            }
            if (this.form.phone == '') {
                this.formFormatters.phoneIsEmpty = true
            } else {
                this.formFormatters.phoneIsEmpty = false
            }
            if (this.form.team_name == '') {
                this.formFormatters.teamNameIsEmpty = true
            } else {
                this.formFormatters.teamNameIsEmpty = false
            }
            if (this.form.team_size == null || this.form.team_size <= 1 ) {
                this.formFormatters.teamSizeIsEmpty = true
            } else {
                this.formFormatters.teamSizeIsEmpty = false
            }

            if (this.formFormatters.captainNameIsEmpty == false &&
            this.formFormatters.groupIsEmpty == false && this.formFormatters.phoneIsEmpty == false && this.formFormatters.teamNameIsEmpty == false && this.formFormatters.teamSizeIsEmpty == false) {
                this.postData("https://www.quiz-on.ru/api/register", this.form).then((response) => {
                if (response.status !== 200) {
                    this.showAlert = true;
                    this.alertHeader = "Ошибка!"
                    this.alertText = "КОД ОТВЕТА НЕ 200"
                } else {
                    this.showAlert = true;
                    this.alertHeader = "Поздравляем!"
                    this.alertText = "ВЫ УСПЕШНО ЗАРЕГИСТРИРОВАНЫ"
                }
            });
            this.form = {
                // userId: userId,
                captain_name: "",
                group: "",
                phone: "",
                team_name: "",
                team_size: null,
            }
            } else {
                this.showAlert = true
                this.alertHeader = 'Пожалуйста,'
                this.alertText = "ЗАПОЛНИТЕ ВСЕ ПОЛЯ ФОРМЫ!"
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

.main {
    margin-top: 30px;
}
.form {
    width: 90vw;
    background-color: #0F1A2E;
    border-radius: 21px;
    margin: auto;
}

.center {
    margin: auto;
}

.header {
    padding-top: 17px;
    box-sizing: border-box;
    font-size: 19px;
    font-family: "Montserrat";
    font-weight: 700;
    color: white;
    width: 80vw;
}

.game_num {
    padding-top: 17px;
    box-sizing: border-box;
    font-size: 21px;
    font-family: "Montserrat";
    font-weight: 700;
    color: #CBA262;
    width: fit-content;
    width: 80vw;
}

.block_input {
    margin-top: 11px;
    width: 80vw;
    height: 51px;
}
.reg_btn {
    margin-top: 12px;
    background: rgba(10, 18, 33, 0.5);
    border: 1.33428px solid #CBA262;
    border-radius: 17.3457px;

    width: 80vw;
    height: 25px;

    font-family: Montserrat;
    font-weight: 700;
    color: #FFFFFF;
}

.btn_container {
    width: 80vw;
    font-size: 12px;
    padding-bottom: 30px;
}

.error_output {
    margin-top: 12px;
    width: 80vw;
    max-width: 80vw;
    font-family: Montserrat;
    font-weight: 400;
    overflow-wrap: break-word;
    color: #9F2128;
}

.block_text {
    font-size: 13px;
    line-height: 15px;
    font-family: Montserrat;
    font-weight: 700;
    color: #FFFFFF;
}

::placeholder {
    font-family: Montserrat;
    font-weight: 400;
    font-size: 12px;
    color: #FFFFFF33;
}

.input {
    padding: 8px;
    margin-top: 6px;
    box-sizing: border-box;
    width: 100%;
    height: 32px;
    border-radius: 12px;
    border-width: 2px;
    background-color: #0A1221;
    border-color: #FFFFFF33;
    color: #FFFFFF;
}

.info {
    display: flex;
    margin-top: 11px;
    width: 80vw;
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
    font-family: Montserrat;
    font-weight: 400;
    font-size: 12px;
    margin-left: 8px;
    margin-top: auto;
    margin-bottom: auto;
}
.agreement {
    margin-top: 20px;
    font-family: Montserrat;
    font-weight: 400;
    font-size: 12px;
    color: white;
}

a {
    color:#CBA262;
    text-decoration: none;
}

.error{
    border-color: #9F2128;
}

</style>