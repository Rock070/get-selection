<script lang="ts">
const initFakeValue = `
在一個小鎮裡，有一個名叫傑克的男孩，他非常熱愛大自然和探險。他總是喜歡探索週圍的森林和山丘，尋找新的冒險和寶藏。

有一天，傑克在森林裡發現了一個神秘的洞穴，他決定探索一下。他帶著裝備和燈光進入了洞穴，發現裡面非常漆黑，他只能倚靠手電筒的光線前進。

當他繼續往前走時，他聽到了一些聲音，似乎有人在他後面跟著他。他回頭一看，發現有一個小精靈跟在他後面。傑克非常驚訝，因為他從來沒有見過這樣的生物。

小精靈告訴傑克，他是來自一個神秘的世界，他們的國王需要傑克的幫助，因為有一個邪惡的巫師企圖佔領他們的王國。傑克瞬間被這個驚人的故事吸引，他毫不猶豫地同意幫助小精靈。

於是，他跟著小精靈前往了那個神秘的世界。在那裡，他遇到了其他的小精靈和一些神奇的生物，他們一起對抗邪惡的巫師。

經過一番努力，傑克和小精靈們終於擊敗了巫師，解救了那個神秘世界的居民。傑克感到非常高興，他從這個冒險中學到了很多東西，也獲得了一些珍貴的寶藏。

回到現實世界，傑克開始想念他在那個神秘世界的冒險。他感謝小精靈們給了他這個難得的機會，他決定將這個故事寫下來，與其他人分享他的冒險旅程。從此以後，傑克變得更加勇敢，他總是懷著對冒險的熱情

回到現實世界後，傑克感謝小精靈們給了他這個難得的機會，也發現了自己的內在力量和勇氣。他開始將這個故事寫下來，希望能與其他人分享他的冒險旅程，也鼓勵更多的人去探索世界和挑戰自己的極限。

在回家的路上，傑克感到非常充實和開心，他發現這次探險不僅讓他獲得了珍貴的寶藏，更重要的是，他學到了很多關於自己和世界的事情。他決定將這些經驗和體悟應用到生活中，讓自己變得更加勇敢和有自信，也希望能啟發更多人去發現自己的潛力和夢想。

傑克回到家中，開始寫下了這個故事。他花了好幾天的時間，用盡所有的創意和想像力，將自己在神秘世界的冒險寫成了一本冒險小說。他希望這個故事能夠讓更多人體驗到他的冒險旅程和充滿挑戰的世界。

當傑克完成這本小說後，他決定將它發布到互聯網上，與全世界的讀者分享。這個故事迅速受到了廣泛的關注，人們讚揚傑克的勇氣和創意，也對這個神秘世界的奇妙和想像力充滿好奇和探究。

在這個過程中，傑克也得到了許多回饋和鼓勵，這讓他更加堅定了自己的夢想和信念。他認為，每個人都有自己的冒險和探索，只要勇敢地面對挑戰和困難，就能找到屬於自己的寶藏和奇妙。他決定繼續探索世界，獲得更多的經驗和體悟，也希望能夠啟發更多人去追尋夢想和挑戰自己。
`
</script>

<script setup lang="ts">
const onAppendTextClick = (value: string) => {
  const newText = ` ${value} `

  if (!window)
    return

  const sel = window.getSelection()

  if (!sel)
    return
  const selectedText = sel.toString()

  // 檢查是否選擇了文字
  if (selectedText) {
    const range = sel.getRangeAt(0)

    range.deleteContents()
    range.insertNode(document.createTextNode(newText))
  }
  else {
    // 如果未選擇文本，請在光標位置插入新文本
    const cursorPosition = sel.getRangeAt(0).startOffset
    const node = sel.getRangeAt(0).startContainer
    const text = node.textContent
    const textBeforeCursor = text?.substring(0, cursorPosition)
    const textAfterCursor = text?.substring(cursorPosition)
    const replacedText = textBeforeCursor + newText + textAfterCursor
    node.textContent = replacedText
  }
}

const list = [
  {
    label: '取代為「城鎮」',
    value: '城鎮',
  },
  {
    label: '取代為「煙囪」',
    value: '煙囪',
  },
  {
    label: '取代為「小屋」',
    value: '小屋',
  },
]
</script>

<template>
  <div>
    <h1 class="px-4 font-bold text-lg mb-5">
      選取左側故事中的一段文字，點擊右側任一個按鈕，將文字取代為指定的內容
    </h1>

    <div class="flex justify-between">
      <article class="section w-[70%]" v-text="initFakeValue" />

      <div class="section flex flex-col grow space-y-3">
        <strong>按鈕</strong>
        <button
          v-for="i in list"
          :key="i.value"
          type="button"
          class="basic-button"
          @click="onAppendTextClick(i.value)"
        >
          {{ i.label }}
        </button>
      </div>
    </div>
  </div>
</template>

<style>
.basic-button {
  @apply px-2 py-1 bg-gray-200 text-gray-700 rounded-md;
  @apply hover:text-white hover:bg-slate-500;
}

.section {
  @apply border border-solid border-gray-300 p-3;
}
</style>
