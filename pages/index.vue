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
                  <v-btn block rounded outlined color="black" @click="add"
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
      <v-card cols="1" v-for="kanji in kanjis" :key="kanji.text">
        <v-list-item>
          <v-col>{{ kanji.text }}</v-col>
          <v-col>{{ kanji.number }}</v-col>
        </v-list-item>
      </v-card>
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
      <v-card
        cols="10"
        sm="10"
        md="10"
        lg="10"
        v-for="result in results2"
        :key="result.text"
      >
        <v-col>{{ result.name }}</v-col>
        <v-col>{{ result.sokaku }}</v-col>
        <v-col>{{ result.jinkaku }}</v-col>
      </v-card>
    </v-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      //古い画数ベース
      kanjis: [
        { text: '識', number: 19 },
        { text: '譜', number: 19 },
        { text: '翼', number: 17 },
        { text: '檎', number: 17 },
        { text: '燦', number: 17 },
        { text: '凛', number: 15 },
        { text: '舞', number: 15 },
        { text: '夢', number: 14 }, //修正??
        { text: '雅', number: 12 }, //修正
        { text: '智', number: 12 },
        { text: '貴', number: 12 },
        { text: '雲', number: 12 },
        { text: '理', number: 12 }, //修正
        { text: '進', number: 15 }, //修正
        { text: '淑', number: 12 }, //修正
        { text: '彩', number: 11 },
        { text: '粋', number: 10 },
        { text: '真', number: 10 },
        { text: '眞', number: 10 },
        { text: '修', number: 10 },
        { text: '晄', number: 10 },
        { text: '華', number: 14 }, //修正
        { text: '律', number: 9 },
        { text: '奏', number: 9 },
        { text: '星', number: 9 },
        { text: '和', number: 8 },
        { text: '怜', number: 9 }, //修正
        { text: '來', number: 8 },
        { text: '歩', number: 7 }, //修正
        { text: '知', number: 8 },
        { text: '宙', number: 8 },
        { text: '征', number: 8 },
        { text: '昊', number: 8 },
        { text: '学', number: 16 }, //修正
        { text: '旺', number: 8 },
        { text: '伶', number: 7 },
        { text: '妙', number: 7 },
        { text: '那', number: 11 }, //修正
        { text: '志', number: 7 },
        { text: '呉', number: 7 },
        { text: '希', number: 7 },
        { text: '考', number: 6 },
        { text: '羽', number: 6 },
        { text: '伎', number: 6 },
        { text: '叶', number: 5 },
        { text: '央', number: 5 },
        { text: '元', number: 4 },
        { text: '円', number: 13 }, //修正
        { text: '水', number: 4 },
        { text: '久', number: 3 },
        { text: '己', number: 3 },
      ],
      //新しい画数ベース
      // kanjis: [
      //   { text: '識', number: 19 },
      //   { text: '譜', number: 19 },
      //   { text: '翼', number: 17 },
      //   { text: '檎', number: 17 },
      //   { text: '燦', number: 17 },
      //   { text: '凛', number: 15 },
      //   { text: '舞', number: 15 },
      //   { text: '夢', number: 13 },
      //   { text: '雅', number: 13 },
      //   { text: '智', number: 12 },
      //   { text: '貴', number: 12 },
      //   { text: '雲', number: 12 },
      //   { text: '理', number: 11 },
      //   { text: '進', number: 11 },
      //   { text: '淑', number: 11 },
      //   { text: '彩', number: 11 },
      //   { text: '粋', number: 10 },
      //   { text: '真', number: 10 },
      //   { text: '眞', number: 10 },
      //   { text: '修', number: 10 },
      //   { text: '晄', number: 10 },
      //   { text: '華', number: 10 },
      //   { text: '律', number: 9 },
      //   { text: '奏', number: 9 },
      //   { text: '星', number: 9 },
      //   { text: '和', number: 8 },
      //   { text: '怜', number: 8 },
      //   { text: '來', number: 8 },
      //   { text: '歩', number: 8 },
      //   { text: '知', number: 8 },
      //   { text: '宙', number: 8 },
      //   { text: '征', number: 8 },
      //   { text: '昊', number: 8 },
      //   { text: '学', number: 8 },
      //   { text: '旺', number: 8 },
      //   { text: '伶', number: 7 },
      //   { text: '妙', number: 7 },
      //   { text: '那', number: 7 },
      //   { text: '志', number: 7 },
      //   { text: '呉', number: 7 },
      //   { text: '希', number: 7 },
      //   { text: '考', number: 6 },
      //   { text: '羽', number: 6 },
      //   { text: '伎', number: 6 },
      //   { text: '叶', number: 5 },
      //   { text: '央', number: 5 },
      //   { text: '元', number: 4 },
      //   { text: '円', number: 4 },
      //   { text: '水', number: 4 },
      //   { text: '久', number: 3 },
      //   { text: '己', number: 3 },
      // ],
      temps: [
        { text: '平', number: 5 },
        { text: '田', number: 5 },
      ],
      results: [],
      results2: [],
      tempName: null,
      random3: null,
      random4: null,
      sokaku: null,
      jinkaku: null,
      goodList: [31, 47],
      goodList2: [8, 13, 18, 21, 23, 31, 38, 41, 47],
      // goodList: [8, 13, 18, 21, 23, 24, 31, 38, 41, 47],
      // goodList2: [8, 13, 18, 21, 23, 31, 38, 41, 47],
    }
  },
  methods: {
    // 使いたい漢字をkanjisに追加
    add() {
      this.kanjis.push({ text: this.kanjis.text, number: this.kanjis.number })
    },
    calculate() {
      for (let i = 0; i < 10000000; i++) {
        // ランダムにkanjisから1文字選んでtemplist3文字目をに入れる
        let count = i / 1000000
        if (Number.isInteger(count)) {
          console.log(i)
        }
        // ランダムにkanjisから1文字選んでtemplist3文字目をに入れる
        this.random3 = Math.floor(Math.random() * this.kanjis.length)
        this.temps.push({
          text: this.kanjis[this.random3].text,
          number: this.kanjis[this.random3].number,
        })
        // ランダムにkanjisから1文字選んでtemplist4文字目を文字目に入れる
        this.random4 = Math.floor(Math.random() * this.kanjis.length)
        this.temps.push({
          text: this.kanjis[this.random4].text,
          number: this.kanjis[this.random4].number,
        })
        //総画計算
        this.sokaku =
          this.temps[0].number +
          this.temps[1].number +
          this.temps[2].number +
          this.temps[3].number
        //人格計算
        this.jinkaku = this.temps[1].number + this.temps[2].number

        //名前を仮格納
        this.tempName = this.temps[2].text + this.temps[3].text
        //総画、人格ともに問題なければリザルトリストに入れる
        if (this.goodList.indexOf(this.sokaku) !== -1) {
          if (this.goodList2.indexOf(this.jinkaku) !== -1) {
            this.results.push({
              name: this.tempName,
              sokaku: this.sokaku,
              jinkaku: this.jinkaku,
            })
          }
        }

        // リフレッシュ処理
        this.random3 = null
        this.random4 = null
        this.temps = [
          { text: '平', number: 5 },
          { text: '田', number: 5 },
        ]
        this.tempName = null
        this.sokaku = 0
        this.jinkaku = 0
      }

      //重複削除ロジック
      this.results2 = this.results.filter(
        (element, index, self) =>
          self.findIndex((e) => e.name === element.name) === index
      )

      // テスト用表示処理
      // console.log(
      //   this.temps[0].text +
      //     this.temps[1].text +
      //     this.temps[2].text +
      //     this.temps[3].text
      // )
      // console.log(this.sokaku)
      // console.log(this.jinkaku)
    },
  },
}
</script>

<style scoped lang="scss">
.center {
  text-align: center;
}
</style>
