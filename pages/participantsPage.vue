<template>
  <div class="main">
    <h1>УЧАСТНИКИ</h1>
    <!-- <client-only>
    <vuetable 
    class="table"
    ref="vuetable"
    :fields="headers"
    :api-mode="false"
    :data="this.rows"
  ></vuetable>
    </client-only> -->

    <div class="container">
  <table class="table">
    <thead>
      <tr>
        <th>Команда</th>
        <th>Телеграм</th>
        <th>ID команды</th>
        <th>Капитан</th>
        <th>Группа</th>
        <th>Телефон</th>
        <th>Участников</th>
      </tr>
    </thead>
    <tbody id="rows">

    </tbody>
  </table>
</div>
  </div>
</template>

<script>

// import Vuetable from 'vuetable-2'


export default {
  components: {
    // Vuetable
  },
  data() {
    return {
      // headers: ['team_name', 'tg_contact', 'team_id', 'captain_name', 'group_name', 'phone', 'amount'],
      // rows: [],
    }
  },
  beforeMount() {
    this.getParticipants('https://www.quiz-on.ru/api/registrations')
    
    
    
  },
  methods: {
    async getParticipants(url) {
      try {
        await fetch(url).then(response => {
          response.json().then(data => {
            console.log(data)
            if (data.length > 0) {
              let temp = "";
                for (const itemData of data) {
                  let teamId = ""
                  if (itemData.team_id) { 
                    teamId = itemData.team_id 
                  }
                  temp += "<tr style='height: 70px; border: solid; border-width: 0.2px 0; border-color: rgba(255, 255, 255, 0.5);'>";
                  temp += "<td style='padding: 10px;'>" + itemData.team_name + "</td>";
                  temp += "<td style='padding: 10px;'>" + itemData.tg_contact + "</td>";
                  temp += "<td style='padding: 10px;'>" + teamId + "</td>";
                  temp += "<td style='padding: 10px;'>" + itemData.captain_name + "</td>";
                  temp += "<td style='padding: 10px;'>" + itemData.group_name + "</td>";
                  temp += "<td style='padding: 10px;'>" + itemData.phone + "</td>";
                  temp += "<td style='padding: 10px;'>" + itemData.amount + "</td>";

                };
                document.getElementById('rows').innerHTML = temp;
            }
          })
        })
      } catch (error) {
        this.showAlert = true;
        this.alertHeader = "Ошибка"
        this.alertText = "при загрузке данных"
      }
    },
    
  }
}


</script>

<style scoped>
h1 {
  padding-bottom: 3vh;
  font-family: ProductSans;
  font-size: 36px;
  font-weight: 700;
  line-height: 36px;
  letter-spacing: 2px;
  text-align: center;
  color: white;
}
table {
  background: #0F1A2E;
  border-radius: 15px;
  border-collapse: collapse;
  margin: 0 auto;
}
th{
  font-family: ProductSans;
  font-size: 15px;
  font-weight: 700;
  line-height: 24px;
  letter-spacing: 0px;
  text-align: left;
  color: #E0AC59;
  padding: 10px;
}
tbody{
  font-family: ProductSans;
  font-size: 15px;
  font-weight: 400;
  line-height: 24px;
  letter-spacing: 0px;
  text-align: left;
  color: white;
}
</style>