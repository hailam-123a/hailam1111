<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <title>Trà My dễ thương</title>
  <style>
    body {
      margin: 0;
      background: black;
    }
    canvas {
      display: block;
    }
  </style>
</head>
<body>
<canvas id="canvas"></canvas>

<script>
  const canvas = document.getElementById("canvas");
  const ctx = canvas.getContext("2d");
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;

  const dots = [];
  const total = 500;
  const scale = 12;
  const centerX = canvas.width / 2;
  const centerY = canvas.height / 2;

  // Tạo vị trí đích theo đường trái tim
  function heartFunction(t) {
    const x = 16 * Math.pow(Math.sin(t), 3);
    const y = 13 * Math.cos(t) - 5 * Math.cos(2 * t) - 2 * Math.cos(3 * t) - Math.cos(4 * t);
    return { x: x * scale + centerX, y: -y * scale + centerY };
  }

  // Tạo dots
  for (let i = 0; i < total; i++) {
    const t = Math.random() * Math.PI * 2;
    const target = heartFunction(t);

    dots.push({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      tx: target.x,
      ty: target.y,
      color: `hsl(${Math.random() * 360}, 100%, 70%)`,
    });
  }

  function animate() {
    ctx.clearRect(0, 0, canvas.width, canvas.height);

    // Vẽ từng dot và di chuyển
    dots.forEach(dot => {
      // Di chuyển dần về vị trí đích
      dot.x += (dot.tx - dot.x) * 0.05;
      dot.y += (dot.ty - dot.y) * 0.05;

      ctx.beginPath();
      ctx.arc(dot.x, dot.y, 4, 0, Math.PI * 2);
      ctx.fillStyle = dot.color;
      ctx.fill();
    });

    // Vẽ chữ
    ctx.fillStyle = "pink";
    ctx.font = "bold 40px Arial";
    const text = "Trà My dễ thương";
    const textWidth = ctx.measureText(text).width;
    ctx.fillText(text, (canvas.width - textWidth) / 2, canvas.height - 60);

    requestAnimationFrame(animate);
  }

  animate();
</script>
</body>
</html>
