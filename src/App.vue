<template>
  <div class="bg-gradient-to-b from-slate-900 to-slate-800 text-white min-h-screen">
    <!-- Header -->
    <header class="fixed w-full bg-slate-900/80 backdrop-blur-lg z-50">
      <nav class="container mx-auto px-6 py-4">
        <div class="flex items-center justify-between">
          <div class="text-2xl font-bold">玄机</div>
          <div class="hidden md:flex space-x-8">
            <a href="#features" class="hover:text-purple-400 transition">特色</a>
            <a href="#how-it-works" class="hover:text-purple-400 transition">工作原理</a>
            <a href="#testimonials" class="hover:text-purple-400 transition">用户评价</a>
            <a href="#pricing" class="hover:text-purple-400 transition">价格</a>
            <a href="#faq" class="hover:text-purple-400 transition">常见问题</a>
          </div>
        </div>
      </nav>
    </header>

    <!-- Hero Section -->
    <section class="pt-32 pb-20 px-6">
      <div class="container mx-auto text-center">
        <h1 class="text-5xl md:text-7xl font-bold mb-8 bg-gradient-to-r from-purple-400 to-pink-400 text-transparent bg-clip-text">
          探索你的命运轨迹
        </h1>
        <p class="text-xl md:text-2xl text-gray-300 mb-12 max-w-3xl mx-auto">
          结合东方玄学、紫微斗数、易经与西方星座学，为您提供专业、精准的运势预测
        </p>
        <div class="max-w-2xl mx-auto bg-white/10 backdrop-blur-lg rounded-2xl p-8">
          <form @submit.prevent="calculateFortune" class="space-y-6">
            <div>
              <input v-model="name" type="text" placeholder="您的姓名" required
                class="w-full px-4 py-3 rounded-lg bg-white/5 border border-gray-600 focus:border-purple-400 focus:outline-none">
            </div>
            <div>
              <input v-model="birthdate" type="date" required
                class="w-full px-4 py-3 rounded-lg bg-white/5 border border-gray-600 focus:border-purple-400 focus:outline-none">
            </div>
            <button type="submit"
              class="w-full bg-gradient-to-r from-purple-500 to-pink-500 py-4 rounded-lg text-lg font-semibold hover:opacity-90 transition">
              开始测算
            </button>
          </form>
        </div>
      </div>
    </section>

    <!-- Features -->
    <section id="features" class="py-20 px-6 bg-slate-800/50">
      <div class="container mx-auto">
        <h2 class="text-4xl font-bold text-center mb-16">专业解析系统</h2>
        <div class="grid md:grid-cols-3 gap-8">
          <div class="bg-white/5 p-8 rounded-2xl">
            <h3 class="text-2xl font-semibold mb-4">东方玄学</h3>
            <p class="text-gray-300">融合八字、五行、紫微斗数等传统东方命理学说，深入解析命盘。</p>
          </div>
          <div class="bg-white/5 p-8 rounded-2xl">
            <h3 class="text-2xl font-semibold mb-4">西方星座</h3>
            <p class="text-gray-300">结合现代占星学理论，分析行星位置对运势的影响。</p>
          </div>
          <div class="bg-white/5 p-8 rounded-2xl">
            <h3 class="text-2xl font-semibold mb-4">AI 分析</h3>
            <p class="text-gray-300">采用先进算法，综合多维度数据，提供精准预测。</p>
          </div>
        </div>
      </div>
    </section>

    <!-- How it Works -->
    <section id="how-it-works" class="py-20 px-6">
      <div class="container mx-auto">
        <h2 class="text-4xl font-bold text-center mb-16">运算流程</h2>
        <div class="grid md:grid-cols-4 gap-8">
          <div class="text-center" v-for="(step, index) in steps" :key="index">
            <div class="w-16 h-16 bg-purple-500 rounded-full flex items-center justify-center mx-auto mb-4">
              {{ index + 1 }}
            </div>
            <h3 class="text-xl font-semibold mb-2">{{ step.title }}</h3>
            <p class="text-gray-300">{{ step.description }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Testimonials -->
    <section id="testimonials" class="py-20 px-6 bg-slate-800/50">
      <div class="container mx-auto">
        <h2 class="text-4xl font-bold text-center mb-16">用户评价</h2>
        <div class="grid md:grid-cols-3 gap-8">
          <div v-for="testimonial in testimonials" :key="testimonial.name" class="bg-white/5 p-8 rounded-2xl">
            <div class="flex items-center mb-4">
              <img :src="testimonial.avatar" :alt="testimonial.name" class="w-12 h-12 rounded-full">
              <div class="ml-4">
                <h4 class="font-semibold">{{ testimonial.name }}</h4>
                <p class="text-gray-400">{{ testimonial.title }}</p>
              </div>
            </div>
            <p class="text-gray-300">{{ testimonial.comment }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Pricing -->
    <section id="pricing" class="py-20 px-6">
      <div class="container mx-auto">
        <h2 class="text-4xl font-bold text-center mb-16">服务价格</h2>
        <div class="grid md:grid-cols-3 gap-8 max-w-5xl mx-auto">
          <div v-for="plan in plans" :key="plan.name"
            :class="['rounded-2xl p-8', plan.featured ? 'bg-gradient-to-b from-purple-500 to-pink-500 transform scale-105' : 'bg-white/5']">
            <h3 class="text-2xl font-semibold mb-4">{{ plan.name }}</h3>
            <p class="text-4xl font-bold mb-8">¥{{ plan.price }}<span class="text-lg" :class="plan.featured ? 'text-gray-200' : 'text-gray-400'">/次</span></p>
            <ul class="space-y-4 mb-8">
              <li v-for="feature in plan.features" :key="feature">✓ {{ feature }}</li>
            </ul>
            <button :class="[
              'w-full py-3 rounded-lg transition',
              plan.featured ? 'bg-white text-purple-600 font-semibold hover:bg-gray-100' : 'bg-white/10 hover:bg-white/20'
            ]">选择方案</button>
          </div>
        </div>
      </div>
    </section>

    <!-- FAQ -->
    <section id="faq" class="py-20 px-6 bg-slate-800/50">
      <div class="container mx-auto max-w-4xl">
        <h2 class="text-4xl font-bold text-center mb-16">常见问题</h2>
        <div class="space-y-8">
          <div v-for="faq in faqs" :key="faq.question" class="bg-white/5 p-6 rounded-xl">
            <h3 class="text-xl font-semibold mb-4">{{ faq.question }}</h3>
            <p class="text-gray-300">{{ faq.answer }}</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="bg-slate-900 py-12 px-6">
      <div class="container mx-auto">
        <div class="grid md:grid-cols-4 gap-8 mb-8">
          <div>
            <h3 class="text-xl font-bold mb-4">玄机</h3>
            <p class="text-gray-400">专业的现代化运势预测平台</p>
          </div>
          <div>
            <h4 class="font-semibold mb-4">快速链接</h4>
            <ul class="space-y-2 text-gray-400">
              <li><a href="#features" class="hover:text-purple-400">特色</a></li>
              <li><a href="#how-it-works" class="hover:text-purple-400">工作原理</a></li>
              <li><a href="#pricing" class="hover:text-purple-400">价格</a></li>
            </ul>
          </div>
          <div>
            <h4 class="font-semibold mb-4">联系我们</h4>
            <ul class="space-y-2 text-gray-400">
              <li>邮箱：ljkcjj@gmail.com</li>
              <li>工作时间：周一至周日 9:00-21:00</li>
            </ul>
          </div>
          <div>
            <h4 class="font-semibold mb-4">关注我们</h4>
            <div class="flex space-x-4">
              <a href="#" class="text-gray-400 hover:text-purple-400">微信</a>
              <a href="#" class="text-gray-400 hover:text-purple-400">微博</a>
              <a href="#" class="text-gray-400 hover:text-purple-400">抖音</a>
            </div>
          </div>
        </div>
        <div class="border-t border-gray-800 pt-8 text-center text-gray-400">
          <p>© 2025 玄机 版权所有 | 维尼</p>
        </div>
      </div>
    </footer>

    <!-- Fortune Result Modal -->
    <div v-if="showModal" class="fixed inset-0 bg-black/50 flex items-center justify-center z-50">
      <div class="bg-slate-800 p-8 rounded-2xl max-w-lg w-full mx-4">
        <h3 class="text-2xl font-bold mb-6">{{ name }}的运势分析</h3>
        
        <div class="mb-6">
          <div class="flex items-center justify-between mb-2">
            <span class="text-gray-300">运势评级</span>
            <span class="text-2xl font-bold text-purple-400">{{ fortuneResult.rating }}</span>
          </div>
          <div class="flex items-center justify-between">
            <span class="text-gray-300">运势分数</span>
            <span class="text-2xl font-bold text-purple-400">{{ fortuneResult.score }}</span>
          </div>
        </div>
        
        <div class="mb-6">
          <h4 class="font-semibold mb-2">宜</h4>
          <p class="text-gray-300">{{ fortuneResult.goods.join('、') }}</p>
        </div>
        
        <div class="mb-6">
          <h4 class="font-semibold mb-2">忌</h4>
          <p class="text-gray-300">{{ fortuneResult.bads.join('、') }}</p>
        </div>
        
        <div class="mb-6">
          <h4 class="font-semibold mb-2">分析依据</h4>
          <ul class="text-gray-300 space-y-2">
            <li v-for="reason in fortuneResult.reasons" :key="reason">• {{ reason }}</li>
          </ul>
        </div>
        
        <button @click="showModal = false"
          class="w-full bg-purple-500 py-3 rounded-lg hover:bg-purple-600 transition">
          关闭
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const name = ref('')
const birthdate = ref('')
const showModal = ref(false)
const fortuneResult = ref({})

const steps = [
  { title: '输入信息', description: '填写基本个人信息' },
  { title: '数据分析', description: '多维度数据计算' },
  { title: '运势生成', description: '生成详细运势报告' },
  { title: '专家解读', description: '提供专业建议指导' }
]

const testimonials = [
  {
    name: '张小姐',
    title: '企业高管',
    avatar: 'https://images.unsplash.com/photo-1438761681033-6461ffad8d80?w=100&h=100&fit=crop',
    comment: '预测非常准确，帮助我在关键时刻做出了正确的决策。专业的分析让我对未来更有信心。'
  },
  {
    name: '王先生',
    title: '创业者',
    avatar: 'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?w=100&h=100&fit=crop',
    comment: '东西方结合的分析方式很新颖，给了我很多启发。建议都很实用，值得信赖。'
  },
  {
    name: '李女士',
    title: '自由职业者',
    avatar: 'https://images.unsplash.com/photo-1544005313-94ddf0286df2?w=100&h=100&fit=crop',
    comment: '分析很全面，不仅告诉你结果，还会解释原因。这种专业度让人很放心。'
  }
]

const plans = [
  {
    name: '基础版',
    price: 68,
    features: [
      '基础运势分析',
      '运势评级',
      '基本建议指导'
    ]
  },
  {
    name: '专业版',
    price: 168,
    featured: true,
    features: [
      '详细运势分析',
      '运势评级与分数',
      '专业建议指导',
      '月度运势预测',
      '电话咨询服务'
    ]
  },
  {
    name: '尊享版',
    price: 368,
    features: [
      '全方位运势分析',
      '运势评级与分数',
      'VIP专属指导',
      '年度运势预测',
      '24小时咨询服务',
      '风水布局建议'
    ]
  }
]

const faqs = [
  {
    question: '运势预测的准确度如何？',
    answer: '我们结合传统东方命理学说与现代占星术，通过大数据分析，准确率可达85%以上。'
  },
  {
    question: '如何保证个人信息安全？',
    answer: '我们采用银行级别的加密技术，确保您的个人信息绝对安全。所有数据都经过严格加密处理。'
  },
  {
    question: '运势分析需要多长时间？',
    answer: '基础版分析在10分钟内完成，专业版和尊享版因为分析更加深入，需要24小时内完成。'
  },
  {
    question: '可以退款吗？',
    answer: '如果您对服务不满意，我们提供7天内无理由退款服务。'
  }
]

function calculateFortune() {
  const goodThings = [
    '投资理财', '谈判合作', '出行旅游', '签订合同',
    '开展新项目', '人际交往', '学习进修', '装修搬家'
  ]
  
  const badThings = [
    '轻率决策', '高风险投资', '改变现状', '冲动消费',
    '激进行动', '争执冲突', '过度劳累', '铺张浪费'
  ]
  
  const reasons = [
    '根据紫微斗数显示，您目前正处于运势上升期',
    '从八字五行分析，您的命盘显示近期贵人相助',
    '结合星座运势，显示您当前处于能量积累阶段',
    '易经卦象显示，您正值转运关键期'
  ]

  const score = Math.floor(Math.random() * 40) + 60
  const ratings = ['A', 'B', 'C', 'D']
  const rating = ratings[Math.floor(score/25)]
  
  fortuneResult.value = {
    rating,
    score,
    goods: goodThings.sort(() => Math.random() - 0.5).slice(0, Math.floor(Math.random() * 2) + 2),
    bads: badThings.sort(() => Math.random() - 0.5).slice(0, Math.floor(Math.random() * 2) + 2),
    reasons: reasons.sort(() => Math.random() - 0.5).slice(0, 2)
  }
  
  showModal.value = true
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@100..900&display=swap');

* {
  font-family: 'Noto Sans SC', sans-serif;
}
</style>