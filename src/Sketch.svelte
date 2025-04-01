<script>
  import P5 from "p5-svelte";

  const sketch = (p5) => {
    // svelte-ignore perf_avoid_nested_class
    class Ball {
      constructor(x, y, radius) {
        this.x = x;
        this.y = y;
        this.radius = radius;
        this.dx = p5.random(-0.5, 0.5);
        this.dy = p5.random(-0.5, 0.5);
      }

      move() {
        this.x += this.dx;
        this.y += this.dy;

        this.x = (width + this.x) % width;
        this.y = (height + this.y) % height;
      }

      draw() {
        p5.fill(0xd9, 0xd9, 0xd9);
        p5.stroke(0xd3, 0xd3, 0xd3);
        p5.circle(this.x, this.y, this.radius);
      }
    }

    let width = 1440;
    let height = 800;

    let nr_balls = 90;
    let ball_array = [];

    p5.setup = () => {
      p5.createCanvas(width, height);
      for (let i = 0; i < nr_balls; i++) {
        ball_array.push(
          new Ball(p5.random(0, width), p5.random(0, height), p5.random(1, 7))
        );
        console.log(ball_array[i]);
      }
    };

    p5.draw = () => {
      p5.background(255, 255, 234);
      for (let i = 0; i < nr_balls; i++) {
        let mouse_d = p5.dist(
          ball_array[i].x,
          ball_array[i].y,
          p5.mouseX,
          p5.mouseY
        );
        if (mouse_d < 1000) {
          p5.stroke(0, 0, 0, 150 - p5.lerp(0, mouse_d, 0.5));
          p5.line(ball_array[i].x, ball_array[i].y, p5.mouseX, p5.mouseY);
        }
        // p5.fill(0xd3, 0xd3, 0xd3);
        // p5.stroke(0xd3, 0xd3, 0xd3);
        // p5.circle(ball_array[i].x, ball_array[i].y, ball_array[i].radius);
        ball_array[i].draw();
        ball_array[i].move();
        for (let j = 0; j < nr_balls - 1; j++) {
          let d = p5.dist(
            ball_array[i].x,
            ball_array[i].y,
            ball_array[j].x,
            ball_array[j].y
          );
          if (d < 300) {
            p5.strokeWeight(1);
            p5.stroke(0xd3, 0xd3, 0xd3, 150 - p5.lerp(0, d, 0.8));
            p5.line(
              ball_array[i].x,
              ball_array[i].y,
              ball_array[j].x,
              ball_array[j].y
            );
          }
        }
      }
    };
  };
</script>

<P5 {sketch} />
