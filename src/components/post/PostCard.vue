<script setup>
defineProps({
  id: Number,
  userName: String,
  title: String,
  content: String,
  hit: Number,
  registerTime: String
})

function elapsedTime(date) {
  const start = new Date(date)
  const end = new Date()

  const diff = (end - start) / 1000

  const times = [
    { name: '년', milliSeconds: 60 * 60 * 24 * 365 },
    { name: '개월', milliSeconds: 60 * 60 * 24 * 30 },
    { name: '일', milliSeconds: 60 * 60 * 24 },
    { name: '시간', milliSeconds: 60 * 60 },
    { name: '분', milliSeconds: 60 }
  ]

  for (const value of times) {
    const betweenTime = Math.floor(diff / value.milliSeconds)

    if (betweenTime > 0) {
      return `${betweenTime}${value.name} 전`
    }
  }
  return '방금 전'
}
</script>

<template>
  <section id="section">
    <div class="upper">
      <div class="info">
        <img
          src="https://t1.kakaocdn.net/kakaocorp/kakaocorp/admin/6562f7bc017800001.png?type=thumb&opt=C72x72.fwebp"
          width="36"
          height="36"
        />
        <div class="state">인기 게시글</div>
        <span class="date">{{ elapsedTime(registerTime) }}</span>
      </div>

      <h1 id="title">{{ title }}</h1>

      <ul id="tag">
        <li>#부산</li>
        <li>#용</li>
        <li>#절</li>
        <li>#108배</li>
      </ul>
    </div>

    <div class="lower"> 내용 : {{ content }} , <br/> 작성자 : {{ userName }} , 조회수 : {{ hit }}</div>
    <!-- <img src="" alt=""> -->
  </section>
</template>

<style scoped>
#section {
  box-sizing: border-box;
  width: 430px;
  height: 380px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  /* border: 1px solid #d6d9d7; */
  border-radius: 15px;
  background-color: var(--font-color);
}

.upper {
  flex-basis: 30%;
  flex-grow: 1;
  padding: 20px;
}
.info {
  display: flex;
  align-items: center;
  gap: 10px;
}
.state {
  padding: 5px 10px;
  font-size: 13px;
  line-height: 20px;
  color: var(--tag-font-color);
  border-radius: 10px;
  background-color: var(--tag-color);
}
.date {
  font-size: 11px;
  line-height: 20px;
  color: var(--tag-font-color);
}

#title {
  margin: 10px 0;
  font-size: 25px;
  color: var(--fourth-font-color);
}

#tag {
  margin: 0;
  padding: 0;
  list-style: none;
  display: flex;
  gap: 5px;
  font-size: 14px;
  line-height: 19px;
  color: var(--tag-font-color);
}

.lower {
  padding: 20px;
  flex-basis: 70%;
  flex-grow: 4;
  background-color: var(--sky-color);
  border-radius: 0 0 15px 15px;
}
</style>
