<script setup lang="ts">
import { ref } from "vue";
const newLocal = ".focus-color";
const height = ref(0);
const weight = ref(0);
const result = ref(0);
function calBmi() {
  result.value = weight.value / (height.value / 100) ** 2;
}
</script>

<template>
  <div style="width: 500px; margin: auto">
    <h1>เครื่องคำนวณหาค่าดัชนีมวลกาย (BMI)</h1>

    <p>
      การหาค่าดัชนีมวลกาย (Body Mass Index : BMI)
      คือเป็นมาตรการที่ใช้ประเมินภาวะอ้วนและผอมในผู้ใหญ่ ตั้งแต่อายุ 20 ปีขึ้นไป
      สามารถทำได้โดยการชั่งน้ำหนักตัวเป็นกิโลกรัม และวัดส่วนสูงเป็นเซนติเมตร
      แล้วนำมาหาดัชมีมวลกาย โดยใช้โปรแกรมวัดค่าความอ้วนข้างต้น
    </p>

    <div>
      <label for="weight">น้ำหนักตัว (kg.)</label>
      <input id="weight" v-model="weight" type="text" />
    </div>

    <div>
      <label for="height">ส่วนสูง (cm.)</label>
      <input id="height" v-model="height" type="text" />
    </div>

    <div><button @click="calBmi">คำนวณ</button></div>

    <div class="result-border">
      <div class="center">BMI</div>
      <div class="center" style="font-size: 25pt">
        {{ result === Infinity ? 0 : result.toFixed(2) }}
      </div>
    </div>
    <table>
      <tr>
        <th>BMI kg/m2</th>
        <th>อยู่ในเกณท์</th>
        <th>ภาวะเสี่ยงต่อโรค</th>
      </tr>
      <tr :class="{ 'focus-color': result < 18.5 }">
        <td>น้อยกว่า 18.50</td>
        <td>น้ำหนักน้อย / ผอม</td>
        <td>มากกว่าคนปกติ</td>
      </tr>
      <tr :class="{ 'focus-color': result >= 18.5 && result < 23 }">
        <td>ระหว่าง 18.50 - 22.90</td>
        <td>ปกติ (สุขภาพดี)</td>
        <td>เท่าคนปกติ</td>
      </tr>
      <tr :class="{ 'focus-color': result >= 23 && result < 25 }">
        <td>ระหว่าง 23 - 24.90</td>
        <td>ท้วม / โรคอ้วนระดับ 1</td>
        <td>อันตรายระดับ 1</td>
      </tr>
      <tr :class="{ 'focus-color': result >= 25 && result < 30 }">
        <td>ระหว่าง 25 - 29.90</td>
        <td>อ้วน / โรคอ้วนระดับ 2</td>
        <td>อันตรายระดับ 2</td>
      </tr>
      <tr :class="{ 'focus-color': result >= 30 }">
        <td>มากกว่า 30</td>
        <td>อ้วนมาก / โรคอ้วนระดับ 3</td>
        <td>อันตรายระดับ 3</td>
      </tr>
    </table>
    <div v-if="result < 18.5">
      <h1>น้ำหนักน้อยกว่ามาตรฐาน</h1>
      <p>
        คุณมีน้ำหนักน้อยหรือผอม โดยทั่วไป ค่าดัชนีมวลกายปกติมีค่าน้อยกว่า 18.50
      </p>
      <ol>
        <li>
          ควรกินอาหารให้หลากหลายครบ 5 หมู่ในสัดส่วนที่เหมาะสมและปริมาณมากขึ้น
          โดยเพิ่มอาหารประเภทที่ให้พลังงานมากขึ้น เช่น ไขมัน แป้ง ข้าว
          เนื้อสัตว์ นม
        </li>
        <li>
          ควรเคลื่อนไหวและออกกำลังกายอย่างสม่ำเสมอทุกวันหรือเกือบทุกวัน
          ให้เหนื่อยพอควรโดยหายใจกระชั้นขึ้น เช่น เดินเร็ว ถีบจักรยาน รำมวยจีน
          ลีลาศจังหวะช้า รวมทั้งงานบ้าน งานสวน เป็นต้น สะสมให้ได้อย่างน้อยวันละ
          30 นาทีอาจไม่จำเป็นต้องออกกำลังกายให้เหนื่อยมากหรือหอบ
          ที่ง่ายที่สุดคือ การเดิน
        </li>
      </ol>
    </div>

    <div v-if="result >= 18.5 && result < 23">
      <h1>น้ำหนักปกติ</h1>
      <h2>ข้อแนะนำ</h2>
      <ol>
        <li>
          ควรกินอาหารให้หลากหลายครบ 5 หมู่ในสัดส่วนที่เหมาะสม
          กินเท่าที่ร่างกายต้องการวันไหนกินมากเกินไป วันต่อมาก็กินลดลง
          กินอาหารพวกข้าวและแป้งรวมทั้งเมล็ดธัญพืชอื่น ๆ
          ให้มากขึ้นไม่น้อยกว่าวันละ 6 ทัพพี กินผัก รวมทั้งเมล็ดถั่ว ผลไม้
          ไม่ต่ำกว่าวันละ 5 ส่วน หรือครึ่งกิโลกรัม
          เพื่อไม่ให้มีพลังงานส่วนเกินจะทำให้ควบคุมน้ำหนักได้ดีและสมดุล
        </li>
        <li>
          ควรเคลื่อนไหวและออกกำลังกายอย่างสม่ำเสมอทุกวัน หรือเกือบทุกวัน
          อย่างน้อยให้เหนื่อยพอควร โดยหายใจกระชั้นขึ้น สะสมให้ได้อย่างน้อยวันละ
          30 นาที โดยอาจจะแบ่งเป็น 2 - 3 ครั้งก็ได้
          จะเป็นกิจกรรมออกกำลังกายที่เป็นเรื่องเป็นราวหรือการออกแรงในกิจวัตรประจำวัน
          เช่นเดินเร็ว ถีบจักรยาน ลีลาศ หรืองานบ้าน งานสวน ให้เลือกทำตามใจชอบ
          ถ้าคุณต้องการมีสมรรถภาพที่ดีก็ต้องออกกำลังกายแบบแอโรบิก เช่น เดินเร็ว
          ๆ วิ่งเหยาะ ถีบจักรยานเร็วๆ กระโดดเชือก ว่ายน้ำ เล่นกีฬา เป็นต้น
          ให้รู้สึกเหนื่อยมาก หรือหอบ อย่างน้อยวันละ 20 - 30 นาที
          อย่างน้อยสัปดาห์ละ 3 วัน ที่ง่าย ที่สุดคือ การเดิน
        </li>
      </ol>
    </div>
    <div v-if="result >= 23 && result < 25">
      <h1>ท้วม / อ้วนระดับ 1</h1>
      <p>
        คุณมี น้ำหนักเกิน หรือรูปร่างท้วม
        โดยทั่วไปค่าดัชนีมวลกายปกติมีค่าระหว่าง 23 - 24.90
      </p>
      <h2>ข้อแนะนำ</h2>
      <ol>
        <li>
          ควรควบคุมอาหาร
          โดยลดปริมาณอาหารหรือปรับเปลี่ยนอาหารจากที่ให้พลังงานมากเป็นอาหารที่ให้พลังงานน้อย
          ทั้งนี้พลังงานที่ได้รับไม่ควรต่ำกว่า 1200 กิโลแคลอรีต่อวัน
          โดยลดอาหารไขมัน/ เนื้อสัตว์ อาหารผัด/ทอด ขนมหวาน
          เครื่องดื่มที่ใส่น้ำตาล แอลกอฮอล์
          แต่ต้องกินอาหารให้หลากหลายในสัดส่วนที่เหมาะสม กินข้าวและแป้ง
          รวมทั้งเมล็ดธัญพืชอื่น ๆ ไม่น้อยกว่าวันละ 6 ทัพพี กินผัก
          รวมทั้งเมล็ดถั่ว ผลไม้ ไม่ต่ำกว่าวันละ 5 ส่วน หรือครึ่งกิโลกรัม
          เพื่อลดพลังงานเข้า
          ร่างกายจะได้ใช้พลังงานส่วนเกินที่สะสมอยู่ในรูปไขมันแทน
        </li>
        <li>
          ควรเคลื่อนไหวและออกกำลังกายแบบแอโรบิกอย่างสม่ำเสมอทุกวัน
          หรือเกือบทุกวันอย่างน้อยให้เหนื่อยพอควร โดยหายใจกระชั้นขึ้น
          สะสมอย่างน้อยวันละ 30 นาที อาจแบ่งเป็นวันละ 2 - 3 ครั้งก็ได้ เช่น
          เดินเร็ว ถีบจักรยาน เป็นต้น หากยังไม่เคยออกกำลังกายเริ่มแรกควร
          ออกกำลังเบา ๆ ที่ง่ายที่สุดคือ การเดิน ใช้เวลาน้อย ๆ ก่อน จากนั้นค่อย
          ๆ เพิ่มเวลาขึ้นในแต่ละสัปดาห์ โดยยังไม่เพิ่มความหนัก
          เมื่อร่างกายปรับตัวได้จึงค่อยเพิ่มความหนัก
          หรือความเหนื่อยตามที่ต้องการ
          และเพิ่มการเคลื่อนไหวร่างกายให้มากขึ้นในชีวิตประจำวัน
          เพื่อให้มีการใช้พลังงานเพิ่มขึ้น อย่างน้อยวันละ 200 - 300 กิโลแคลอรี
        </li>
        <li>
          ควรฝึกความแข็งแรงของกล้ามเนื้อ ด้วยการฝึกกายบริหารหรือยกน้ำหนัก
          จะช่วยเสริมให้ร่างกายมีการใช้พลังงานเพิ่มมากขึ้น ทำให้ไขมันลดลง
        </li>
      </ol>
    </div>

    <div v-if="result >= 25 && result < 30">
      <h1>อ้วน / อ้วนระดับ 2</h1>
      <p>
        คุณ อ้วนแล้ว (อ้วนระดับ 2) โดยทั่วไปค่าดัชนีมวลกายปกติมีค่าระหว่าง 25 -
        29.90
      </p>
      <h2>ข้อแนะนำ</h2>
      <ol>
        <li>
          ควรควบคุมอาหารโดยลดปริมาณอาหารหรือปรับเปลี่ยนอาหารจากที่ให้พลังงานมากเป็นอาหารที่ให้พลังงานน้อย
          ทั้งนี้พลังงานที่ได้รับไม่ควรต่ำกว่า 1200 กิโลแคลอรีต่อวัน
          โดยลดอาหารไขมัน/เนื้อสัตว์ อาหารผัด/ทอด ขนมหวาน
          เครื่องดื่มที่ใส่น้ำตาล แอลกอฮอล์
          แต่ต้องกินอาหารให้หลากหลายในสัดส่วนที่เหมาะสม
          กินข้าวและแป้งรวมทั้งเมล็ดธัญพืชอื่น ๆ ไม่น้อยกว่าวันละ 6 ทัพพี
          กินผักรวมทั้งเมล็ดถั่ว ผลไม้ไม่ต่ำกว่าวันละ 5 ส่วน
          หรือครึ่งกิโลกรัมเพื่อลดพลังงานเข้า
          ร่างกายจะได้ใช้พลังงานส่วนเกินที่สะสมอยู่ในรูปไขมันแทน
        </li>
        <li>
          ควรเคลื่อนไหวและออกกำลังกายแบบแอโรบิกอย่างสม่ำเสมอทุกวันหรือเกือบทุกวันอย่างน้อยให้เหนื่อยพอควรโดยหายใจกระชั้นขึ้น
          ประมาณ 40-60 นาทีต่อวัน หรือแบ่งเป็นวันละ 2 ครั้ง ๆ ละ 20 - 30 นาที
          เช่น เดินเร็ว ถีบจักรยาน เป็นต้น หากยังไม่เคยออกกำลังกายเริ่มแรก
          ควรออกกำลังเบา ๆ ที่ง่ายที่สุดคือ การเดิน ใช้เวลาน้อยๆ ก่อน จากนั้น
          ค่อย ๆ เพิ่มเวลาขึ้นในแต่ละสัปดาห์ โดยยังไม่เพิ่มความหนัก
          เมื่อร่างกายปรับตัวได้จึงค่อยเพิ่มความหนัก
          หรือความเหนื่อยตามที่ต้องการและเพิ่มการเคลื่อนไหวร่างกายให้มากขึ้นในชีวิตประจำวัน
          เพื่อให้มีการใช้พลังงานเพิ่มขึ้น อย่างน้อยวันละ 200 - 300 กิโลแคลอรี
        </li>
        <li>
          ควรฝึกความแข็งแรงของกล้ามเนื้อ ด้วยการฝึกกายบริหารหรือยกน้ำหนัก
          จะช่วยเสริมให้ร่างกายมีการใช้พลังงานเพิ่มมากขึ้น ทำให้ไขมันลดลง
        </li>
        <li>
          ถ้าคุณสามารถลดพลังงานเข้าจากอาหารลงได้วันละ 400 กิโลแคลอรี
          และเพิ่มการใช้ พลังงานจากการออกกำลังกายวันละ 200 กิโลแคลอรี
          รวมแล้วคุณมีพลังงาพร่องลงไปวันละ 600 กิโลแคลอรี ออกกำลังกายประมาณ 6
          วัน คิดเป็นพลังงานพร่อง 3600 กิโลแคลอรี
          คุณจะลดไขมันลงได้ประมาณครึ่งกิโลกรัมต่อสัปดาห์ พลังงานเข้าหรือออก 3500
          กิโลแคลอรี จะเพิ่มหรือลดไขมันได้ 1 ปอนด์ หรือ 0.45 กิโลกรัม
        </li>
        <li>ควรปรึกษาแพทย์หรือผู้เชี่ยวชาญในการลดและควบคุมน้ำหนัก</li>
      </ol>
    </div>

    <div v-if="result >= 30">
      <h1>อ้วนมาก / อ้วนระดับ 3</h1>
      <p>
        คุณ อ้วนมากแล้ว (อ้วนระดับ 3) โดยทั่วไปค่าดัชนีมวลกายปกติมีค่ามากกว่า 30
      </p>
      <h2>ข้อแนะนำ</h2>
      <ol>
        <li>
          ควรควบคุมอาหารโดยลดปริมาณอาหารหรือปรับเปลี่ยนอาหารจากที่ให้พลังงานมากเป็นอาหารที่ให้พลังงานน้อย
          ทั้งนี้พลังงานที่ได้รับไม่ควรต่ำกว่า 1200 กิโลแคลอรีต่อวัน
          โดยลดอาหารไขมัน/เนื้อสัตว์ อาหารผัด/ทอด ขนมหวาน
          เครื่องดื่มที่ใส่น้ำตาล แอลกอฮอล์
          แต่ต้องกินอาหารให้หลากหลายในสัดส่วนที่เหมาะสม
          กินข้าวและแป้งรวมทั้งเมล็ดธัญพืชอื่น ๆ ไม่น้อยกว่าวันละ 6 ทัพพี
          กินผักรวมทั้งเมล็ดถั่ว ผลไม้ไม่ต่ำกว่าวันละ 5 ส่วน
          หรือครึ่งกิโลกรัมเพื่อลดพลังงานเข้า
          ร่างกายจะได้ใช้พลังงานส่วนเกินที่สะสมอยู่ในรูปไขมันแทน
        </li>
        <li>
          ควรเคลื่อนไหวและออกกำลังกายแบบแอโรบิกอย่างสม่ำเสมอทุกวันหรือเกือบทุกวันอย่างน้อยให้เหนื่อยพอควรโดยหายใจกระชั้นขึ้น
          ประมาณ 40-60 นาทีต่อวัน หรือแบ่งเป็นวันละ 2 ครั้ง ๆ ละ 20 - 30 นาที
          เช่น เดินเร็ว ถีบจักรยาน เป็นต้น หากยังไม่เคยออกกำลังกายเริ่มแรก
          ควรออกกำลังเบา ๆ ที่ง่ายที่สุดคือ การเดิน ใช้เวลาน้อยๆ ก่อน จากนั้น
          ค่อย ๆ เพิ่มเวลาขึ้นในแต่ละสัปดาห์ โดยยังไม่เพิ่มความหนัก
          เมื่อร่างกายปรับตัวได้จึงค่อยเพิ่มความหนัก
          หรือความเหนื่อยตามที่ต้องการและเพิ่มการเคลื่อนไหวร่างกายให้มากขึ้นในชีวิตประจำวัน
          เพื่อให้มีการใช้พลังงานเพิ่มขึ้น อย่างน้อยวันละ 200 - 300 กิโลแคลอรี
        </li>
        <li>
          ควรฝึกความแข็งแรงของกล้ามเนื้อ ด้วยการฝึกกายบริหารหรือยกน้ำหนัก
          จะช่วยเสริมให้ร่างกายมีการใช้พลังงานเพิ่มมากขึ้น ทำให้ไขมันลดลง
        </li>
        <li>
          ถ้าคุณสามารถลดพลังงานเข้าจากอาหารลงได้วันละ 400 กิโลแคลอรี
          และเพิ่มการใช้ พลังงานจากการออกกำลังกายวันละ 200 กิโลแคลอรี
          รวมแล้วคุณมีพลังงาพร่องลงไปวันละ 600 กิโลแคลอรี ออกกำลังกายประมาณ 6
          วัน คิดเป็นพลังงานพร่อง 3600 กิโลแคลอรี
          คุณจะลดไขมันลงได้ประมาณครึ่งกิโลกรัมต่อสัปดาห์ พลังงานเข้าหรือออก 3500
          กิโลแคลอรี จะเพิ่มหรือลดไขมันได้ 1 ปอนด์ หรือ 0.45 กิโลกรัม
        </li>
        <li>ควรปรึกษาแพทย์หรือผู้เชี่ยวชาญในการลดและควบคุมน้ำหนัก</li>
      </ol>
    </div>
  </div>
</template>

<style scoped>
.center {
  text-align: center;
}

.focus-color {
  background-color: rgb(254, 205, 165);
}

input[type="text"] {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
  text-align: center;
}

div {
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
}

button {
  width: 100%;
  background-color: #4caf50;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

button:hover {
  background-color: #4caf50;
}

.result-border {
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

th,
td {
  padding: 15px;
  text-align: left;
  border-bottom: 1px solid #ddd;
}
</style>
