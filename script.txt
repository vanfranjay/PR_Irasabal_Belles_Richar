function* counterGenerator(N, A) {
  let counters = new Array(N).fill(0);
  let currentMin = 0;
  let maxCounter = 0;

  for (const operation of A) {
    if (operation >= 1 && operation <= N) {
      const index = operation - 1;
      counters[index] = Math.max(counters[index], currentMin) + 1;
      maxCounter = Math.max(maxCounter, counters[index]);
    } else if (operation === N + 1) {
      currentMin = maxCounter;
    }
    yield counters.map((counter) => Math.max(counter, currentMin));
  }
}

const solution = (N, A) => {
  const finalCounters = [...counterGenerator(N, A)].pop();
  return finalCounters;
};

function calcular() {
  const n = parseInt(document.getElementById("n").value);
  const a = document.getElementById("a").value.split(",").map(Number);

  const finalCounters = solution(n, a);

  document.getElementById("resultado").innerHTML =
    "Resultado: [" + finalCounters.join(", ") + "]";
  console.log(finalCounters);
}

const A = [1, 1, 4, 6, 1, 5, 5];
const N = 5;
const result = solution(N, A);
console.log(result);