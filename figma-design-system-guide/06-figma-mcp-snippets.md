# Figma MCP 자동화 스크립트

본 가이드의 규칙들은 Figma MCP(`use_figma`)를 통해 자동화할 수 있다. 아래는 자주 쓰이는 스크립트 모음.

## 흰색 카드 프레임 적용 스크립트 (페이지 단위)

해당 페이지의 모든 자식을 감싸는 흰색 카드 프레임을 생성하고 100px 패딩을 적용한다.
스펙은 [02-frame-and-layout.md#흰색-카드-프레임-스펙](02-frame-and-layout.md#흰색-카드-프레임-스펙) 참조.

```javascript
const page = figma.currentPage;
const children = [...page.children];
let minX = Infinity, minY = Infinity, maxX = -Infinity, maxY = -Infinity;

children.forEach(n => {
  minX = Math.min(minX, n.x);
  minY = Math.min(minY, n.y);
  maxX = Math.max(maxX, n.x + n.width);
  maxY = Math.max(maxY, n.y + n.height);
});

const padding = 100;
const cardFrame = figma.createFrame();
cardFrame.name = page.name.replace(/^\d+ — /, ''); // 번호 제거한 이름
cardFrame.x = 0;
cardFrame.y = 0;
cardFrame.resize(
  (maxX - minX) + padding * 2,
  (maxY - minY) + padding * 2
);
cardFrame.fills = [{ type: 'SOLID', color: { r: 1, g: 1, b: 1 } }];
cardFrame.cornerRadius = 16;
cardFrame.effects = [{
  type: 'DROP_SHADOW',
  color: { r: 0.102, g: 0.098, b: 0.086, a: 0.08 }, // #1A1916 = (26, 25, 22) / 255
  offset: { x: 0, y: 4 },
  radius: 16,
  spread: 0,
  visible: true,
  blendMode: 'NORMAL'
}];

for (const node of children) {
  const newX = node.x - (minX - padding);
  const newY = node.y - (minY - padding);
  cardFrame.appendChild(node);
  node.x = newX;
  node.y = newY;
}
```
