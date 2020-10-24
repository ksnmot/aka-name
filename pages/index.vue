<template>
  <div>
    <!-- 漢字登録フィールド-->
    <v-row justify="center" align="center">
      <v-col cols="12" sm="10" justify="center">
        <v-card>
          <v-card-text>
            <!-- 漢字入力 -->
            <v-row>
              <v-col>
                <div class="center">
                  <h2>Step1.使用したい漢字を登録する</h2>
                </div>
                <v-form ref="form">
                  <v-text-field v-model="kanjis.text" label="漢字">
                  </v-text-field>
                  <v-text-field v-model="kanjis.number" label="画数">
                  </v-text-field>
                  <v-btn block rounded outlined color="black" @click="submit"
                    >-登録-</v-btn
                  >
                </v-form>
              </v-col>
            </v-row>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <!-- 登録漢字一覧-->
    <v-row justify="center" align="center">
      <v-col cols="12" sm="10" justify="center">
        <v-card>
          <v-row justify="center" align="center">
            <v-card cols="1" v-for="kanji in kanjis" :key="kanji.text">
              <v-list-item>
                <v-col>{{ kanji.text }}</v-col>
                <v-col>{{ kanji.number }}</v-col>
              </v-list-item>
            </v-card>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
    <!-- 計算ボタン-->
    <v-row justify="center" align="center">
      <v-col cols="12" sm="10" justify="center">
        <v-card>
          <v-card-text>
            <v-row justify="center" align="center">
              <v-col>
                <div class="center">
                  <h2>Step2.画数計算する</h2>
                </div>
              </v-col>
            </v-row>
            <v-row justify="center" align="center">
              <v-col>
                <v-btn block rounded outlined color="black" @click="calculate"
                  >-計算-</v-btn
                >
              </v-col>
            </v-row>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <!-- 名前候補一覧-->
    <v-row justify="center" align="center">
      <v-col cols="12" sm="10" justify="center">
        <v-card>
          <v-row justify="center" align="center">
            <v-card
              cols="2"
              sm="1"
              v-for="result in results"
              :key="result.text"
            >
              <v-list-item row="2">
                <v-col>{{ result.text }}</v-col>
                <v-col>{{ result.number }}</v-col>
              </v-list-item>
            </v-card>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      kanjis: [
        { text: '識', number: 19 },
        { text: '譜', number: 19 },
        { text: '理', number: 11 },
        { text: '進', number: 11 },
        { text: '淑', number: 11 },
        { text: '彩', number: 11 },
        { text: '律', number: 9 },
        { text: '奏', number: 9 },
        { text: '星', number: 9 },
        { text: '希', number: 7 },
        { text: '考', number: 6 },
        { text: '叶', number: 5 },
      ],
      templist: [
        { text: '平', number: 5 },
        { text: '田', number: 5 },
      ],
      results: [],
    }
  },
  methods: {
    submit() {
      this.kanjis.push({ text: this.kanjis.text, number: this.kanjis.number })
      console.log(this.kanjis.text)
    },
    calculate() {
      for (let i = 0; i < this.kanjis.length; i++) {
        console.log(this.kanjis[i])
        if (this.kanjis[i].number < 9) {
          this.results.push({
            text: this.kanjis[i].text,
            number: this.kanjis[i].number,
          })
        }
      }
    },
  },
}
</script>

<style scoped lang="scss">
.center {
  text-align: center;
}
</style>
