<template>
  <div class="questionnaire-wrapper">
    <div class="question-card">
      <h2 class="title">📝 问卷调查表</h2>
      <p class="subtitle">感谢您抽出宝贵时间填写本次问卷</p>

      <div v-if="hasSubmitted" class="submitted-tip">
        <p>✅ 您已完成问卷填写，感谢参与！</p>
      </div>

      <form v-else @submit.prevent="submitForm">
        <div class="item">
          <label class="label"><span class="required">*</span>您的姓名</label>
          <input v-model="form.name" type="text" class="input" placeholder="请输入姓名" required />
        </div>

        <div class="item">
          <label class="label"><span class="required">*</span>您的性别</label>
          <div class="radio-group">
            <label><input v-model="form.gender" value="男" type="radio" name="gender" required /> 男</label>
            <label><input v-model="form.gender" value="女" type="radio" name="gender" /> 女</label>
          </div>
        </div>

        <div class="item">
          <label class="label">您的年龄</label>
          <select v-model="form.age" class="select">
            <option value="">请选择</option>
            <option>18岁以下</option>
            <option>18岁</option>
            <option>19岁</option>
            <option>20岁</option>
            <option>21岁以上</option>
          </select>
        </div>

        <div class="item">
          <label class="label"><span class="required">*</span>你对班长的满意度</label>
          <div class="radio-group">
            <label><input v-model="form.satisfyMonitor" value="非常满意" type="radio" name="satisfyMonitor" required /> 非常满意</label>
            <label><input v-model="form.satisfyMonitor" value="满意" type="radio" name="satisfyMonitor" /> 满意</label>
            <label><input v-model="form.satisfyMonitor" value="一般" type="radio" name="satisfyMonitor" /> 一般</label>
            <label><input v-model="form.satisfyMonitor" value="不满意" type="radio" name="satisfyMonitor" /> 不满意</label>
          </div>
        </div>

        <div class="item">
          <label class="label"><span class="required">*</span>你对副班长的满意度</label>
          <div class="radio-group">
            <label><input v-model="form.satisfyViceMonitor" value="非常满意" type="radio" name="satisfyViceMonitor" required /> 非常满意</label>
            <label><input v-model="form.satisfyViceMonitor" value="满意" type="radio" name="satisfyViceMonitor" /> 满意</label>
            <label><input v-model="form.satisfyViceMonitor" value="一般" type="radio" name="satisfyViceMonitor" /> 一般</label>
            <label><input v-model="form.satisfyViceMonitor" value="不满意" type="radio" name="satisfyViceMonitor" /> 不满意</label>
          </div>
        </div>

        <div class="item">
          <label class="label"><span class="required">*</span>你对学习委员的满意度</label>
          <div class="radio-group">
            <label><input v-model="form.satisfyStudy" value="非常满意" type="radio" name="satisfyStudy" required /> 非常满意</label>
            <label><input v-model="form.satisfyStudy" value="满意" type="radio" name="satisfyStudy" /> 满意</label>
            <label><input v-model="form.satisfyStudy" value="一般" type="radio" name="satisfyStudy" /> 一般</label>
            <label><input v-model="form.satisfyStudy" value="不满意" type="radio" name="satisfyStudy" /> 不满意</label>
          </div>
        </div>

        <div class="item">
          <label class="label"><span class="required">*</span>你对团支书的满意度</label>
          <div class="radio-group">
            <label><input v-model="form.satisfyLeague" value="非常满意" type="radio" name="satisfyLeague" required /> 非常满意</label>
            <label><input v-model="form.satisfyLeague" value="满意" type="radio" name="satisfyLeague" /> 满意</label>
            <label><input v-model="form.satisfyLeague" value="一般" type="radio" name="satisfyLeague" /> 一般</label>
            <label><input v-model="form.satisfyLeague" value="不满意" type="radio" name="satisfyLeague" /> 不满意</label>
          </div>
        </div>

        <div class="item">
          <label class="label"><span class="required">*</span>你对组织委员的满意度</label>
          <div class="radio-group">
            <label><input v-model="form.satisfyOrganize" value="非常满意" type="radio" name="satisfyOrganize" required /> 非常满意</label>
            <label><input v-model="form.satisfyOrganize" value="满意" type="radio" name="satisfyOrganize" /> 满意</label>
            <label><input v-model="form.satisfyOrganize" value="一般" type="radio" name="satisfyOrganize" /> 一般</label>
            <label><input v-model="form.satisfyOrganize" value="不满意" type="radio" name="satisfyOrganize" /> 不满意</label>
          </div>
        </div>

        <div class="item">
          <label class="label">你的兴趣爱好（可多选）</label>
          <div class="checkbox-group">
            <label><input v-model="form.hobbies" value="跑步" type="checkbox" /> 跑步</label>
            <label><input v-model="form.hobbies" value="羽毛球" type="checkbox" /> 羽毛球</label>
            <label><input v-model="form.hobbies" value="篮球" type="checkbox" /> 篮球</label>
            <label><input v-model="form.hobbies" value="足球" type="checkbox" /> 足球</label>
            <label><input v-model="form.hobbies" value="阅读" type="checkbox" /> 阅读</label>
            <label><input v-model="form.hobbies" value="画画" type="checkbox" /> 画画</label>
            <label><input v-model="form.hobbies" value="唱歌" type="checkbox" /> 唱歌</label>
            <label><input v-model="form.hobbies" value="健身" type="checkbox" /> 健身</label>
            <label><input v-model="form.hobbies" value="游戏" type="checkbox" /> 游戏</label>
            <label><input v-model="form.hobbies" value="旅游" type="checkbox" /> 旅游</label>
          </div>
        </div>

        <div class="item">
          <label class="label"><span class="required">*</span>您对未来的规划（40-100字）</label>
          <textarea 
            v-model="form.desc" 
            rows="3" 
            class="textarea" 
            placeholder="请输入规划（40-100字）"
            maxlength="100"
            required
          ></textarea>
          <div class="word-count">已输入：{{ form.desc.length }} / 100 字</div>
        </div>

        <div class="btn-box">
          <button type="submit" class="submit-btn">提交问卷</button>
          <button type="button" @click="reset" class="reset-btn">重新填写</button>
        </div>
      </form>
    </div>

    <div v-if="showSuccess" class="success-tip">✅ 提交成功！感谢参与</div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const form = ref({
  name: '',
  gender: '',
  age: '',
  satisfyMonitor: '',
  satisfyViceMonitor: '',
  satisfyStudy: '',
  satisfyLeague: '',
  satisfyOrganize: '',
  hobbies: [],
  desc: ''
})

const showSuccess = ref(false)
const hasSubmitted = ref(false)

onMounted(() => {
  const flag = localStorage.getItem('questionnaire_submitted')
  if (flag === 'true') {
    hasSubmitted.value = true
  }
})

const submitForm = () => {
  const len = form.value.desc.trim().length
  if (len < 40) {
    alert('未来规划不能少于40字，请补充内容')
    return
  }

  showSuccess.value = true
  hasSubmitted.value = true
  localStorage.setItem('questionnaire_submitted', 'true')
  alert('提交成功！')
}

const reset = () => {
  form.value = {
    name: '',
    gender: '',
    age: '',
    satisfyMonitor: '',
    satisfyViceMonitor: '',
    satisfyStudy: '',
    satisfyLeague: '',
    satisfyOrganize: '',
    hobbies: [],
    desc: ''
  }
}
</script>

<style scoped>
.questionnaire-wrapper {
  max-width: 700px;
  margin: 30px auto;
  padding: 0 20px;
  font-family: "Microsoft YaHei", sans-serif;
}
.question-card {
  background: #fff;
  border-radius: 12px;
  padding: 30px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.07);
}
.title {
  text-align: center;
  font-size: 24px;
  margin: 0;
}
.subtitle {
  text-align: center;
  color: #666;
  margin-bottom: 30px;
}
.item {
  margin-bottom: 22px;
}
.label {
  display: block;
  margin-bottom: 10px;
  font-weight: 500;
  color: #333;
}
.required {
  color: red;
}
.input, .select, .textarea {
  width: 100%;
  padding: 10px 12px;
  border: 1px solid #ddd;
  border-radius: 6px;
  box-sizing: border-box;
  font-size: 14px;
}
.textarea {
  resize: vertical;
}
.word-count {
  font-size: 12px;
  color: #666;
  margin-top: 4px;
  text-align: right;
}
.radio-group, .checkbox-group {
  display: flex;
  gap: 18px;
  flex-wrap: wrap;
}
.btn-box {
  display: flex;
  gap: 15px;
  margin-top: 10px;
}
.submit-btn {
  flex: 1;
  background: #409eff;
  color: #fff;
  border: none;
  padding: 12px;
  border-radius: 6px;
  cursor: pointer;
}
.reset-btn {
  padding: 12px 20px;
  border: 1px solid #ddd;
  background: #f5f5f5;
  border-radius: 6px;
  cursor: pointer;
}
.success-tip {
  text-align: center;
  padding: 15px;
  background: #e6ffed;
  color: #00b42a;
  border-radius: 8px;
  margin: 20px 0;
}
.submitted-tip {
  text-align: center;
  padding: 40px 20px;
  color: #666;
  font-size: 18px;
}
</style>