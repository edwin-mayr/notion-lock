<!doctype html>Add commentMore actions
<html lang="en">
  <head>
    <!-- Required meta tags -->
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <!-- Bootstrap CSS -->
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/3.1.2/rollups/aes.js"></script>
    <title>Notion - Texto encriptado</title>
  </head>
  <body>
      <div class="container p-3">
        <div>
            <label>Password</label>
            <input class="form-control" name="password" id="password" type="password">
        </div>
        <div>
            <label>Text to Encrypt/Decrypt</label>
            <textarea class="form-control" id="text" rows="10"></textarea>
        </div>
        <div class="form-check">
            <input class="form-check-input" type="radio" name="option" id="optionEncrypt">
            <label class="form-check-label" for="optionEncrypt">
                Encrypt Text
            </label>
        </div>
        <div class="form-check">
            <input class="form-check-input" type="radio" name="option" id="optionDecrypt">
            <label class="form-check-label" for="optionDecrypt">
                Decrypt Text
            </label>
        </div>
        <div>
            <button id="go" type="button" class="btn btn-primary">Generate Text</button>
            <button onclick="copy()" type="button" class="btn btn-success ml-4">Copy to clipboard</button>
        </div>
        <h1 class="mt-1">Result:</h1>
        <div id="result" style='white-space:pre'>
            
        </div>
      </div>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>
    <script type="text/javascript">
        var senha = document.getElementById("password");
        var text = document.getElementById("text");

        const encrypt = (texto) => {
            var encrypted = CryptoJS.AES.encrypt(texto, senha.value);
            return encrypted;
        }

        const decrypt = (texto) => {
            var decrypted = CryptoJS.AES.decrypt(texto, senha.value);
            return decrypted.toString(CryptoJS.enc.Utf8);
        }

        var button = document.getElementById("go");
        button.onclick = () => {
            var option = document.querySelector('input[name="option"]:checked')
            if (option.id == "optionEncrypt") {
                var result = encrypt(text.value).toString();
                document.getElementById("result").innerHTML = result;
            }
            if (option.id == "optionDecrypt") {
                var result = decrypt(text.value);
                document.getElementById("result").innerHTML = result;
            }
        }

        var copy = () => {
            if (!navigator.clipboard) {
                var resultArea = document.getElementById("result");
                resultArea.focus();
                resultArea.select();
                document.execCommand('copy');
                return;
            }
            navigator.clipboard.writeText(document.getElementById("result").innerHTML);
        }
    </script>
  </body>
</html>
