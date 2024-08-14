<script setup>
import { ref, computed } from 'vue'
import MarkdownIt from 'markdown-it'
import mdKatex from '@traptitech/markdown-it-katex'
import { katex } from "@mdit/plugin-katex";
import mila from 'markdown-it-link-attributes'
import hljs from 'highlight.js'

const mdi = new MarkdownIt({
  linkify: true,
  highlight(code, language) {
    const validLang = !!(language && hljs.getLanguage(language))
    if (validLang) {
      const lang = language ?? ''
      return highlightBlock(hljs.highlight(code, { language: lang }).value, lang)
    }
    return highlightBlock(hljs.highlightAuto(code).value, '')
  },
})

mdi.use(mila, { attrs: { target: '_blank', rel: 'noopener' } })
mdi.use(mdKatex, { blockClass: 'katexmath-block rounded-3xl p-[10px]', errorColor: ' #cc0000' })
mdi.use(katex); // 只要加了这一行就报错
function highlightBlock(str, lang) {
  
  return `<pre class="code-block-wrapper"><div class="code-block-header"><div class="left"><div class="circle bg1"></div><div class="circle bg2"></div><div class="circle bg3"></div></div><div class="right"><span class="code-block-header__lang">${lang}</span><span class="code-block-header__copy">${t('chat.copyCode')}</span></div></div><code class="hljs code-block-body ${lang}">${str}</code></pre>`
}

const text = computed(() => {
  const value = "伯努利方程是流体力学中的一个重要方程，描述了理想流体沿流线流动时的能量守恒关系。下面是伯努利方程的详细推导过程：\n\n### 1. **基本假设**\n我们假设流体是**不可压缩**的，且是**无粘性**的，同时流体沿着一条**流线**（streamline）流动。伯努利方程其实是基于能量守恒定律（机械能守恒定律）推导出来的。\n\n### 2. **流体沿流线的一小段**\n考虑流体沿流线流动，选取其中的一小段管道，长度为 \\(ds\\)。我们关心的是这段流体元的能量变化情况。\n\n- 设流体的密度为 \\(\\rho\\)。\n- 流体在这段管道入口的速度为 \\(v\\)，出口的速度为 \\(v + dv\\)。\n- 入口处的压强为 \\(p\\)，出口处的压强为 \\(p + dp\\)。\n- 入口处的高度为 \\(z\\)，出口处的高度为 \\(z + dz\\)。\n\n### 3. **动能的变化**\n流体在这段中的动能变化是：\n\n$$\n\\text{动能变化} = \\frac{1}{2} \\rho v^2 \\cdot dA \\cdot ds \\quad \\text{（入口动能）} - \\frac{1}{2} \\rho (v + dv)^2 \\cdot dA \\cdot ds \\quad \\text{（出口动能）}\n$$\n\n由于 \\(v + dv\\) 较小，展开并忽略二次小量，得到：\n\n$$\nd(\\text{动能}) = \\rho v \\cdot dv \\cdot dA \\cdot ds\n$$\n\n### 4. **势能的变化**\n流体在这段中的势能变化为：\n\n$$\nd(\\text{势能}) = \\rho g z \\cdot dA \\cdot ds \\quad \\text{（入口势能）} - \\rho g (z + dz) \\cdot dA \\cdot ds \\quad \\text{（出口势能）}\n$$\n\n同样展开并忽略二次小量，得到：\n\n$$\nd(\\text{势能}) = -\\rho g \\cdot dz \\cdot dA \\cdot ds\n$$\n\n### 5. **压力能的变化**\n流体在这段中的压力能变化为：\n\n$$\nd(\\text{压力能}) = p \\cdot dA \\cdot ds \\quad \\text{（入口压力能）} - (p + dp) \\cdot dA \\cdot ds \\quad \\text{（出口压力能）}\n$$\n\n展开并忽略二次小量，得到：\n\n$$\nd(\\text{压力能}) = -dp \\cdot dA \\cdot ds\n$$\n\n### 6. **能量守恒**\n根据能量守恒定律，动能、势能和压力能之和的变化应该为零：\n\n$$\nd(\\text{动能}) + d(\\text{势能}) + d(\\text{压力能}) = 0\n$$\n\n代入上面各项变化：\n\n$$\n\\rho v \\cdot dv \\cdot dA \\cdot ds - \\rho g \\cdot dz \\cdot dA \\cdot ds - dp \\cdot dA \\cdot ds = 0\n$$\n\n### 7. **伯努利方程的形式**\n将上式两边同时除以 \\(\\rho \\cdot dA \\cdot ds\\)，并将动能、势能和压强项分开：\n\n$$\nv \\cdot dv - g \\cdot dz - \\frac{dp}{\\rho} = 0\n$$\n\n将各项积分（注意，\\(v\\)、\\(z\\)、\\(p\\)都是沿着流线变化的函数）：\n\n$$\n\\int v \\cdot dv + \\int \\frac{dp}{\\rho} + \\int g \\cdot dz = 0\n$$\n\n积分得到：\n\n$$\n\\frac{v^2}{2} + \\frac{p}{\\rho} + gz = \\text{常数}\n$$\n\n这个方程就是**伯努利方程**，它表明沿流线的每一点，动能、势能和压力能的总和是常数。\n\n### 8. **结论**\n伯努利方程的推导基于流体在无外力作用下沿流线流动时能量守恒的原理。它在实际应用中非常有用，尤其是在工程流体力学中，用于分析流体在管道、喷嘴等设备中的行为。" + "伯努利方程是流体力学中的一个基本方程，描述了理想流体在沿流线流动时，能量守恒的情况。以下是伯努利方程的详细推导过程：\n\n### 1. 基本假设\n\n1. **理想流体**：无粘性、不可压缩流体。\n2. **稳态流动**：流体性质不随时间变化。\n3. **沿流线的流动**：流体在同一流线上。\n\n### 2. 连续性方程\n\n在一个稳态、不可压缩的流动中，流体的质量守恒要求：\n\n\\[ \\frac{\\partial \\rho}{\\partial t} + \\nabla \\cdot (\\rho \\mathbf{v}) = 0 \\]\n\n对于不可压缩流体，\\(\\rho\\)（密度）是常数，简化为：\n\n\\[ \\nabla \\cdot \\mathbf{v} = 0 \\]\n\n### 3. 动量定律\n\n根据流体的动量守恒，考虑一个体积元素 \\(\\delta V\\)，并应用纳维-斯托克斯方程的简化形式（无粘性）：\n\n\\[ \\rho \\left( \\frac{\\partial \\mathbf{v}}{\\partial t} + \\mathbf{v} \\cdot \\nabla \\mathbf{v} \\right) = -\\nabla p + \\rho \\mathbf{g} \\]\n\n在稳态流动中，\\(\\frac{\\partial \\mathbf{v}}{\\partial t} = 0\\)，简化为：\n\n\\[ \\rho (\\mathbf{v} \\cdot \\nabla \\mathbf{v}) = -\\nabla p + \\rho \\mathbf{g} \\]\n\n### 4. 应用速度梯度\n\n使用向量恒等式：\n\n\\[ \\mathbf{v} \\cdot \\nabla \\mathbf{v} = \\nabla \\left( \\frac{1}{2} v^2 \\right) - \\mathbf{v} \\times (\\nabla \\times \\mathbf{v}) \\]\n\n对于无旋流体（即流线是无旋的），\\(\\nabla \\times \\mathbf{v} = 0\\)，因此：\n\n\\[ \\mathbf{v} \\cdot \\nabla \\mathbf{v} = \\nabla \\left( \\frac{1}{2} v^2 \\right) \\]\n\n将其代入动量方程：\n\n\\[ \\rho \\nabla \\left( \\frac{1}{2} v^2 \\right) = -\\nabla p + \\rho \\mathbf{g} \\]\n\n### 5. 积分并整理\n\n对方程两边进行积分，得到：\n\n\\[ \\nabla \\left( \\frac{1}{2} v^2 + \\frac{p}{\\rho} + gz \\right) = 0 \\]\n\n其中，\\(gz\\) 是流体的重力势能项，\\(z\\) 是垂直方向的坐标，\\(g\\) 是重力加速度。\n\n### 6. 伯努利方程\n\n因为梯度 \\(\\nabla\\) 为零，所以上述公式可以写为常数：\n\n\\[ \\frac{1}{2} v^2 + \\frac{p}{\\rho} + gz = C \\]\n\n这里的 \\(C\\) 是常数，可以在不同流线中取不同值，但对于单一流线来说，它是常数。因此：\n\n\\[ \\frac{1}{2} v^2 + \\frac{p}{\\rho} + gz = \\text{常数} \\]\n\n这就是**伯努利方程**。它描述了沿流线的总能量（动能、压力能和位能）守恒的原理。"
  return mdi.render(value)
})

</script>

<template>
  <div v-html="text"></div>
  
</template>

<style >
.katex-html {
  display: none;
}
</style>
