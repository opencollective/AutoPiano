¿Odias el 996? Ven aquí y relájate ~

最近 用 Vue + Tone.js 做 了 一款 钢琴 类 web 应用 ， 名字 定 为 自由 钢琴 （AutoPiano） ， 人生 如 音乐 ， 欢快 且 自由。

此文 权 当作 该 项目 的 总结 和 分享 ~

项目 简介
自由 钢琴 （AutoPiano） 是 利用 HTML5 技术 开发 的 在线 钢琴 应用 ， 致力于 为 钢琴 爱好者 、 音乐 爱好者 以及 其他 的 的 创造 者 提供 一个 优雅 、 简洁 的 平台 ， 在 学习 工作之余 可以 享受 钢琴 、 音乐 的美好。 就 类似于 多年前 Flash 开发 的 钢琴 游戏 ， 自由 钢琴 只是 换 了 H5 的 技术 ， 同时 支持 了 钢琴 曲 的自动 播放功能。

AutoPiano 支持 键盘 按键 和 鼠标 点击 播放 ， 同时 琴键 上 会有 按键 和 音名 提示。 另外 ， AutoPiano 还有 教学 的 功能 ， 一种 方式 是快速入门， 通过 简易 的 谱子 按键 进行 演奏 ， 另 一种 是演奏示例， 通过 钢琴 的自动 播放 来 达到 演示 的 目的。 目前 这 两个 功能 都 在 持续 完善 中 ， 如下 图 所示 ：

autopiano.png

体验 地址 ：http://www.autopiano.cn

项目 地址 ：https://github.com/WarpPrism/AutoPiano

Desarrollador Construir y ejecutar 开发 构建 和 运行
git clone https://github.com/WarpPrism/AutoPiano.git
cd AutoPiano
cnpm install / npm install / yarn install
# development mode -> http://localhost:5000
cnpm run dev
# production mode
cnpm run build

# How to run
1. build project successfully
2. cd dist
3. cnpm install -g anywhere
4. anywhere (using static server to serve the assets)
开发 这样 的 应用 需要 乐理知识 吗？
当然。 基本 的 乐理知识 还是 要 知道 的 ， 比如 CDEFGAB 音名 、 五线谱 、 调 式 、 节奏 等等 还是 要 懂 一点 的。 篇幅 所 限 ， 这里 就不 展开 讨论 了 ， 推荐 两个 网站 ：

https://www.bilibili.com/video/av12168119/
https://www.cnblogs.com/devymex/p/3385179.html
其他 的 就是 编程 知识 了 ， 以及 如何 将 乐理知识 转化 为 程序 逻辑 。AutoPiano 目前 采用 的 技术 架构 是 vue 框架 + tone.js。

钢琴 界面 效果 是 怎么 写 的？
可以 用 CSS 或 贴图。 笔者 这里 直接 用 css 实现 了 ， 考虑 到 钢琴 有 黑 键 和 白 键 ， 且 黑 键 和 白 键 有序 地 排列成 7: 5 的 模式 ， 所以 实现 起来 并不 复杂。

< div  class = " piano-key-wrap " > 
  < div  class = " piano-key wkey " v-for = " note in Notes " : key = " note.keyCode " : data-keyCode = " note.keyCode " v -si = " note.type == 'blanco' " @Haga clic =" clickPianoKey ($ evento, note.keyCode) " > </ div > 
  < div  clase =" tecla B-wrap tecla B-wrap1 "> 
    < clase div = " tecla de piano bkey " v-for = " nota en notas " : key = " note.keyCode " : data-keyCode = " note.keyCode " v-if = " note.type == 'negro' && nota. id> = 36 && note.id <= 40 " @click =" clickPianoKey ($ event, note.keyCode) " > </ div > 
  </ div > 
</ div >
. piano-wrap { ancho : 90 % ; margen : 20 px automático;
  . piano-key-wrap {
     ancho : 100 % ;
    fondo: @ c-black ;
    desbordamiento : oculto;
    posición : relativa;
    . wkey {
       display : inline-block;
      ancho : 2.775 % ;
      altura : 100 % ;
      margen : 0 automático;
      fondo : gradiente lineal (blanco 10 % ,  rgb ( 251 ,  251 ,  251 ) 92 % ,  rgb ( 220 ,  220 ,  220 ) 93 % , blanco 97% );
      borde : sólido 1 px  @ c-negro ;
      radio del borde : 0  0  5 px  5 px ;
      posición : relativa;
      & : active {
         background : linear-gradient ( # eee  10 % ,  # ddd  60 % ,  # bbb  93 % ,  # ccc  97 % );
      }
    }
    . wkey-active {
       background : linear-gradient ( # eee  10 % ,  # ddd  60 % ,  # bbb  93 % ,  # ccc  97 % );
    }
    . bkey-wrap {
       ancho : 20 % ;
      altura : 0 ;
      posición : absoluta;
      arriba : 0 ;
    }
    . bkey-wrap1 { izquierda : 0 ;}
    . bkey-wrap2 { izquierda : 19,5 % ;}
    . bkey-wrap3 { izquierda : 39 % ;}
    . bkey-wrap4 { izquierda : 58,3 % ;}
    . bkey-wrap5 { izquierda : 77,7 % ;}
    . bkey {
       display : inline-block;
      ancho : 10 % ;
      altura : 70 % ;
      fondo : gradiente lineal ( # 000  10 % ,  rgb ( 86 ,  86 ,  86 ) 85 % ,  # 000  90 % );
      radio del borde : 0  0  3 px  3 px ;
      posición: absoluto;
      arriba : 0 ;
      desbordamiento : oculto;
      & : active {
         background : linear-gradient ( rgb ( 86 ,  86 ,  86 ) 10 % ,  # 000  90 % ,  # 222  100 % );
      }
    }
    . bkey-active {
       background : linear-gradient ( rgb ( 86 ,  86 ,  86 ) 10 % ,  # 000  90 % ,  # 222  100 % );
    }
    . bkey : nth-child ( 1 ) { izquierda : 9 % ;}
    . bkey : nth-child ( 2 ) { izquierda : 23 % ;}
    . bkey : nth-child ( 3 ) { izquierda : 50 % ;}
    . bkey : nth-child ( 4 ) { izquierda : 65 % ;}
    . bkey : nth-child ( 5 ) { izquierda : 79 % ;}
  }
}
codepen 上 也 有 很多 这样 的 例子 供 参考 ， 不一定 采用 上述 实现 ：

https://codepen.io/search/pens?q=piano&page=1&order=popularity&depth=everything

相信 只要 合理 地 控制 css 变量 和 数值 ， 大家 能 做出 更好 的 Piano 界面。

如何 实现 单个 音符 的 播放？
实现 音频 播放 ， 最 简单 的 就是 利用 HTML5 中 的audio标签 ， 通过 触发 audio 的 和 pause 方法 ， 实现 对 音频 的 控制 ， 笔者 一 开始 就是 这么 实现 的。

// <div class="audios-wrap" id="audios-wrap">
//   <audio src="" id="preloadAudio" ref="preloadAudio"></audio>
// </div>

// 预先为每个音符都建立一个audio元素
initAudioDom() {
  var vm = this
  for (let i = 0; i< vm.Notes.length; i++) {
    var note = vm.Notes[i]
    $('.audios-wrap').append(`<audio src='${note.url}' hidden='true' data-id='audio${i}' class='audioEle'>`);
  }
},
// 触发某个audio元素的播放
playNote(url) {
  var vm = this
  if (!url || typeof url != 'string') return;
  var audios = $('.audioEle');
  for (let i = 0; i< audios.length; i++) {
    let audio = audios[i];
    if (audio.src.indexOf(url) > -1) {
      var cloneAudioNode = audio.cloneNode()
      cloneAudioNode.play()
      cloneAudioNode.remove()
      break;
    }
  }
}
上述是我的第一种实现方式，即不同音符触发不同audio的播放。之后也许是出于好奇，尝试了 Tone.js，通过Tone.js + 内置采样器实现对音频播放更有效的控制，当然，其提供的很多复杂功能都还没用上。。。

// 初始化 合成 器
esto . sintetizador  =  SmapleLibrary . cargar ( { 
  instrumentos : "piano" 
} ) . toMaster ( )

// 合成 器 触发 音频 释放
playNote ( notename  =  'C4' ,  duration  =  '2n' ) { 
  if  ( ! this . synth )  devuelve 
  esto . sintetizador . triggerAttackRelease (nombre del nombre ,  duración ) ; 
}
嗯 ， 现在 的 代码 就 符合 音乐 美学 和 代码 美学 了 ， 美滋滋。 当然 笔者 也 期望 Tone.js 能 快点 完善 中文 文档 ， 不然 上手 还是 很 吃力 的 ， 感兴趣 的 小 伙伴 可以 先去 其 官 网 一番 一番。

关于 钢琴 曲 的 自动 播放
这一 部分 应该 是 开发 整个 应用 最难 的 地方 了 ， 因为 音乐 或者 说 乐谱 本身 是 相当 复杂 的 ， 根据 百度 的 的 描述 ， 五线谱 起源 于 希腊 ， 历经 上 千年 不断 完善 才 成为 现在 的 乐谱 标准。 简谱 简谱出现 则要 晚 的 多 ， 但 依然 五脏俱全 ， 可以 说 ， 简谱 也不 简单。

笔者 的 实现 思路 是 ， 以 一种 乐谱 格式 为 载体 ， 将 乐谱 转换 为 一种 程序 可 识别 的 格式 ， 然后 导入 到 程序 中 进行 播放 ， 这种 可 识别 格式 如下 所示 ， 目前 目前 所 采用 的 ： ：

  {
    name: '小星星',
    step: 'C',
    speed: '100',
    playState: '',
    mainTrack: ['1(1)',' 1(1)',' 5(1)',' 5(1)',' 6(1)',' 6(1)',' 5(2)',' 4(1)',' 4(1)',' 3(1)',' 3(1)',' 2(1)',' 2(1)',' 1(2)',' 5(1)',' 5(1)',' 4(1)',' 4(1)',' 3(1)',' 3(1)',' 2(2)',' 5(1)',' 5(1)',' 4(1)',' 4(1)',' 3(1)',' 3(1)',' 2(2)',' 1(1)',' 1(1)',' 5(1)',' 5(1)',' 6(1)',' 6(1)',' 5(2)',' 4(1)',' 4(1)',' 3(1)',' 3(1)',' 2(1)',' 2(1)',' 1(2)',
                '1<(1)', '1<(1)', '5<(1)', '5<(1)', '6<(1)', '6<(1)', '5<(2)', '4<(1)', '4<(1)', '3<(1)', '3<(1)', '2<(1)', '2<(1)', '1<(2)', '5<(1)', '5<(1)', '4<(1)', '4<(1)', '3<(1)', '3<(1)', '2<(2)', '5<(1)', '5<(1)', '4<(1)', '4<(1)', '3<(1)', '3<(1)', '2<(2)', '1<(1)', '1<(1)', '5<(1)', '5<(1)', '6<(1)', '6<(1)', '5<(2)', '4<(1)', '4<(1)', '3<(1)', '3<(1)', '2<(1)', '2<(1)', '1<(2)'],
    backingTrack: ['1>(0.5)', '5>(0.5)', '3>(0.5)', '5>(0.5)', '1>(0.5)', '5>(0.5)', '3>(0.5)', '5>(0.5)', '1>(0.5)', '6>(0.5)', '4>(0.5)', '6>(0.5)', '1>(0.5)', '5>(0.5)', '3>(0.5)', '5>(0.5)', '1>(0.5)', '6>(0.5)', '4>(0.5)', '6>(0.5)', '1>(0.5)', '5>(0.5)', '3>(0.5)', '5>(0.5)', '7>>(0.5)', '5>(0.5)', '2>(0.5)', '5>(0.5)', '1>(0.5)', '5>(0.5)', '3>(0.5)', '5>(0.5)', '1>(0.5)', '3>(0.5)', '5>(0.5)',' 1(0.5)', '1>(0.5)', '4>(0.5)', '6>(0.5)',' 1(0.5)', '1>(0.5)', '3>(0.5)', '5>(0.5)',' 1(0.5)', '5>>(0.5)', '7>>(0.5)', '2>(0.5)', '5>(0.5)',
                  '1>(0.5)', '3>(0.5)', '5>(0.5)',' 1(0.5)', '1>(0.5)', '4>(0.5)', '6>(0.5)',' 1(0.5)', '1>(0.5)', '3>(0.5)', '5>(0.5)',' 1(0.5)', '5>>(0.5)', '7>>(0.5)', '2>(0.5)', '5>(0.5)', '1>(0.5)', '5>(0.5)', '3>(0.5)', '5>(0.5)', '1>(0.5)', '5>(0.5)', '3>(0.5)', '5>(0.5)', '1>(0.5)', '6>(0.5)', '4>(0.5)', '6>(0.5)', '1>(0.5)', '5>(0.5)', '3>(0.5)', '5>(0.5)', '1>(0.5)', '6>(0.5)', '4>(0.5)', '6>(0.5)', '1>(0.5)', '5>(0.5)', '3>(0.5)', '5>(0.5)', '7>>(0.5)', '5>(0.5)', '2>(0.5)', '5>(0.5)', '1>(0.5)', '5>(0.5)', '3>(0.5)', '5>(0.5)',

                  '1(0.75)', '5(0.25)', '3(0.5)', '5(0.5)', '1(0.75)', '5(0.25)', '3(0.5)', '5(0.5)', '1(0.75)', '6(0.25)', '4(0.5)', '6(0.5)', '1(0.75)', '5(0.25)', '3(0.5)', '5(0.5)', '1(0.75)', '6(0.25)', '4(0.5)', '6(0.5)', '1(0.75)', '5(0.25)', '3(0.5)', '5(0.5)', '7>(0.75)', '5(0.25)', '2(0.5)', '5(0.5)', '1(0.75)', '5(0.25)', '3(0.5)', '5(0.5)', '1(0.75)', '3(0.25)', '5(0.5)', '1<(0.5)', '1(0.75)', '4(0.25)', '6(0.5)', '1<(0.5)', '1(0.75)', '3(0.25)', '5(0.5)', '1<(0.5)', '5>(0.75)', '7>(0.25)', '2(0.5)', '5(0.5)',
                  '1(0.75)', '3(0.25)', '5(0.5)', '1<(0.5)', '1(0.75)', '4(0.25)', '6(0.5)', '1<(0.5)', '1(0.75)', '3(0.25)', '5(0.5)', '1<(0.5)', '5>(0.75)', '7>(0.25)', '2(0.5)', '5(0.5)', '1(0.75)', '5(0.25)', '3(0.5)', '5(0.5)', '1(0.75)', '5(0.25)', '3(0.5)', '5(0.5)', '1(0.75)', '6(0.25)', '4(0.5)', '6(0.5)', '1(0.75)', '5(0.25)', '3(0.5)', '5(0.5)', '1(0.75)', '6(0.25)', '4(0.5)', '6(0.5)', '1(0.75)', '5(0.25)', '3(0.5)', '5(0.5)', '7>(0.75)', '5(0.25)', '2(0.5)', '5(0.5)', '1>(2)']
  }
额 ， 是 不是 很 复杂 ， 很 臃肿 。。。 它 以 简谱 为 载体 ， 通过 特殊 符号 来 标记 音高 和 时 长 ， 从而 产生 mainTrack 和 backingTrack 两个 音轨 ， 然后 同步 播放 即可。 这种 实现 虽然 ，但 有 很多 致命 缺点 ：

不 兼容 通用 的 计算机 乐谱 格式 ， 如 musicxml
不能 完全 表示 音乐 的 所有 维度 ， 比如 很多 钢琴 谱 不止 有 两个 音轨
过于 抽象 和 复杂 ， 不 实用 ， 很难 制作 这种 识别 格式
音乐 专业 人士 ： ¿qué estás? 弄 啥 嘞？
所以 笔者 转向 另 一种 实现 思路 ，解析 musicxml， 但 奈何 这个 过程 耗时 耗力 ， 目前 只 完成 了 一半 ， 部分 细节 还 没有 完全 解析 正确 ， 如果 读者 有 好的 想法 ， 可以 在 评论 区 留言 探讨。

欢迎 贡献 协作
贡献 代码 ， 直接 PR
贡献 首页 展示 的 随机 歌词 ：https://github.com/WarpPrism/AutoPiano/issues/12
贡献 快速 入门 的 弹奏 方法 ：https://github.com/WarpPrism/AutoPiano/issues/9
没 想到 短时间内 能 有 这么 多 estrella (｀ ・ ω ・ ´) ， 吓得 晚上 下班 回去 又 继续 码 代码 。。。 不过 此 项目 完善 ， 还在 不断 更新 中 ， 特别 是 入门 弹奏 谱子 比较少 ， 目前 只有 ：

小 星星
新年 好
因为 爱情
隐形 的 翅膀
蒲公英 的 约定
纸 短 情 长
同桌 的 你
晴天
千 与 千寻 主题 曲
明天 你好
青花瓷
...
都是 笔者 一个 一个 手 打 出来 的 T_T ， 能力 有限 ， 会 的 就 这么 多 ， 所以 是 时候 见证社区的力量了。

HORQUILLA 时 ， 请 遵循 GPL 开源 协议。

最后
最后 再贴 一下 体验 地址 ：> 体验 地址 ：http://www.autopiano.cn

欢迎 体验 ， 分享。

解析 musicxml 的 过程 仍在 进行 中 ， 如果 某 一天 成功 了 ， 那么示例 演奏里面 就会 加入 海量 的 歌曲 ， 以 供 学习 ， 如果 失败 了 ， 额 ， 那 就是 因为 生活 了 我 奋进 的 脚步 。。。

1554105945684.jpg

原创 不易 ， 转载 分享 时 请 注明 出处 ~

Lanzamientos
