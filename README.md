<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Solveur Mathématique</title>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; margin: 20px; }
        input { width: 80%; padding: 10px; margin: 10px; }
        button { padding: 10px 20px; background: #4CAF50; color: white; border: none; cursor: pointer; }
        #result { margin: 20px; padding: 10px; border: 1px solid #ddd; }
    </style>
</head>
<body>
    <h1>🔢 Solveur Mathématique Simple</h1>
    <p>Entrez une équation (ex: <code>2x + 5 = 11</code>) :</p>
    <input type="text" id="equation" placeholder="Ex: 3x - 7 = 8">
    <br>
    <button onclick="solve()">Résoudre</button>
    <div id="result"></div>

    <script>
        function solve() {
            const equation = document.getElementById("equation").value;
            const resultDiv = document.getElementById("result");

            if (!equation) {
                resultDiv.innerHTML = "<p>⚠️ Entrez une équation !</p>";
                return;
            }

            // Résolution simple (pour les équations linéaires)
            if (equation.includes("x") && equation.includes("=")) {
                try {
                    // Exemple : 2x + 5 = 11 → 2x = 6 → x = 3
                    const parts = equation.split("=");
                    const left = parts[0].trim(); // "2x + 5"
                    const right = parts[1].trim(); // "11"

                    // Remplace "x" par "*x" pour l'éval (ex: "2x" → "2*x")
                    const leftEval = left.replace(/(\d+)x/g, "$1*x").replace(/x/g, "*x");
                    
                    // Résolution basique (pour démo)
                    let xValue;
                    if (leftEval.includes("*x")) {
                        const numPart = leftEval.split("*x")[0];
                        const num = eval(numPart);
                        const rightNum = eval(right);
                        xValue = (rightNum - eval(leftEval.replace("*x", "*0"))) / num;
                        resultDiv.innerHTML = `<p>✅ Solution : <strong>x = ${xValue}</strong></p>`;
                    } else {
                        resultDiv.innerHTML = "<p>❌ Format non supporté. Essayez '3x + 2 = 8'</p>";
                    }
                } catch (e) {
                    resultDiv.innerHTML = `<p>❌ Erreur : ${e.message}</p>`;
                }
            } else {
                resultDiv.innerHTML = "<p>❌ Entrez une équation avec 'x' et '=' (ex: 2x + 3 = 7)</p>";
            }
        }
    </script>
</body>
</html>
