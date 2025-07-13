# pip install pyperclip

import tkinter as tk
from tkinter import ttk, messagebox
import random
import string
import pyperclip

class PasswordGenerator:
    def __init__(self, root):
        self.root = root
        self.root.title("🔐 Generatore Password Avanzato")
        self.root.geometry("500x600")
        self.root.configure(bg='#1a1a2e')
        self.root.resizable(False, False)
        
        # Variabili
        self.length_var = tk.IntVar(value=12)
        self.include_symbols = tk.BooleanVar(value=True)
        self.include_special = tk.BooleanVar(value=True)
        self.include_numbers = tk.BooleanVar(value=True)
        self.password_var = tk.StringVar()
        
        self.setup_ui()
        
    def setup_ui(self):
        # Stile personalizzato
        style = ttk.Style()
        style.theme_use('clam')
        
        # Colori moderni
        style.configure('Title.TLabel', 
                       background='#1a1a2e', 
                       foreground='#00d4ff',
                       font=('Helvetica', 20, 'bold'))
        
        style.configure('Modern.TLabel', 
                       background='#1a1a2e', 
                       foreground='#ffffff',
                       font=('Helvetica', 11))
        
        style.configure('Modern.TCheckbutton', 
                       background='#1a1a2e', 
                       foreground='#ffffff',
                       font=('Helvetica', 10))
        
        # Titolo principale
        title_frame = tk.Frame(self.root, bg='#1a1a2e', pady=20)
        title_frame.pack(fill='x')
        
        title_label = ttk.Label(title_frame, text="🔐 Generatore Password", style='Title.TLabel')
        title_label.pack()
        
        subtitle_label = ttk.Label(title_frame, text="Crea password sicure e personalizzate", style='Modern.TLabel')
        subtitle_label.pack(pady=(5, 0))
        
        # Frame principale
        main_frame = tk.Frame(self.root, bg='#16213e', padx=30, pady=20)
        main_frame.pack(fill='both', expand=True, padx=20, pady=10)
        
        # Sezione lunghezza password
        length_frame = tk.Frame(main_frame, bg='#16213e')
        length_frame.pack(fill='x', pady=(0, 20))
        
        length_label = ttk.Label(length_frame, text="Lunghezza Password:", style='Modern.TLabel')
        length_label.pack(anchor='w')
        
        # Slider per la lunghezza
        length_slider_frame = tk.Frame(length_frame, bg='#16213e')
        length_slider_frame.pack(fill='x', pady=(10, 0))
        
        self.length_slider = tk.Scale(length_slider_frame, 
                                     from_=6, to=25, 
                                     orient='horizontal',
                                     variable=self.length_var,
                                     bg='#16213e',
                                     fg='#ffffff',
                                     activebackground='#00d4ff',
                                     troughcolor='#0f3460',
                                     highlightbackground='#16213e',
                                     font=('Helvetica', 10))
        self.length_slider.pack(fill='x')
        
        # Valore corrente
        self.length_display = ttk.Label(length_frame, text=f"Caratteri: {self.length_var.get()}", style='Modern.TLabel')
        self.length_display.pack(anchor='w', pady=(5, 0))
        
        # Aggiorna display quando slider cambia
        self.length_slider.configure(command=self.update_length_display)
        
        # Sezione opzioni
        options_frame = tk.Frame(main_frame, bg='#16213e')
        options_frame.pack(fill='x', pady=(0, 20))
        
        options_label = ttk.Label(options_frame, text="Opzioni di Generazione:", style='Modern.TLabel')
        options_label.pack(anchor='w', pady=(0, 10))
        
        # Checkbox per simboli
        symbols_check = tk.Checkbutton(options_frame,
                                      text="🔣 Includi Simboli (!@#$%^&*)",
                                      variable=self.include_symbols,
                                      bg='#16213e',
                                      fg='#ffffff',
                                      selectcolor='#0f3460',
                                      activebackground='#16213e',
                                      activeforeground='#00d4ff',
                                      font=('Helvetica', 10))
        symbols_check.pack(anchor='w', pady=2)
        
        # Checkbox per caratteri speciali
        special_check = tk.Checkbutton(options_frame,
                                      text="✨ Includi Caratteri Speciali ({}[]|\\:;\"'<>,.?/)",
                                      variable=self.include_special,
                                      bg='#16213e',
                                      fg='#ffffff',
                                      selectcolor='#0f3460',
                                      activebackground='#16213e',
                                      activeforeground='#00d4ff',
                                      font=('Helvetica', 10))
        special_check.pack(anchor='w', pady=2)
        
        # Checkbox per numeri
        numbers_check = tk.Checkbutton(options_frame,
                                      text="🔢 Includi Numeri (0-9)",
                                      variable=self.include_numbers,
                                      bg='#16213e',
                                      fg='#ffffff',
                                      selectcolor='#0f3460',
                                      activebackground='#16213e',
                                      activeforeground='#00d4ff',
                                      font=('Helvetica', 10))
        numbers_check.pack(anchor='w', pady=2)
        
        # Pulsante genera password
        generate_btn = tk.Button(main_frame,
                                text="🎲 Genera Password",
                                command=self.generate_password,
                                bg='#00d4ff',
                                fg='#1a1a2e',
                                font=('Helvetica', 12, 'bold'),
                                padx=20,
                                pady=10,
                                border=0,
                                cursor='hand2')
        generate_btn.pack(pady=(0, 20))
        
        # Effetto hover per il pulsante
        generate_btn.bind("<Enter>", lambda e: generate_btn.config(bg='#0099cc'))
        generate_btn.bind("<Leave>", lambda e: generate_btn.config(bg='#00d4ff'))
        
        # Campo password generata
        password_frame = tk.Frame(main_frame, bg='#16213e')
        password_frame.pack(fill='x', pady=(0, 20))
        
        password_label = ttk.Label(password_frame, text="Password Generata:", style='Modern.TLabel')
        password_label.pack(anchor='w', pady=(0, 10))
        
        # Entry per mostrare la password
        self.password_entry = tk.Entry(password_frame,
                                      textvariable=self.password_var,
                                      font=('Courier', 12),
                                      bg='#0f3460',
                                      fg='#ffffff',
                                      insertbackground='#00d4ff',
                                      state='readonly',
                                      justify='center')
        self.password_entry.pack(fill='x', pady=(0, 10), ipady=8)
        
        # Pulsanti azione
        buttons_frame = tk.Frame(password_frame, bg='#16213e')
        buttons_frame.pack(fill='x')
        
        copy_btn = tk.Button(buttons_frame,
                            text="📋 Copia",
                            command=self.copy_password,
                            bg='#28a745',
                            fg='#ffffff',
                            font=('Helvetica', 10, 'bold'),
                            padx=15,
                            pady=5,
                            border=0,
                            cursor='hand2')
        copy_btn.pack(side='left', padx=(0, 10))
        
        clear_btn = tk.Button(buttons_frame,
                             text="🗑️ Cancella",
                             command=self.clear_password,
                             bg='#dc3545',
                             fg='#ffffff',
                             font=('Helvetica', 10, 'bold'),
                             padx=15,
                             pady=5,
                             border=0,
                             cursor='hand2')
        clear_btn.pack(side='left')
        
        # Effetti hover per i pulsanti
        copy_btn.bind("<Enter>", lambda e: copy_btn.config(bg='#218838'))
        copy_btn.bind("<Leave>", lambda e: copy_btn.config(bg='#28a745'))
        clear_btn.bind("<Enter>", lambda e: clear_btn.config(bg='#c82333'))
        clear_btn.bind("<Leave>", lambda e: clear_btn.config(bg='#dc3545'))
        
        # Indicatore di sicurezza
        self.security_frame = tk.Frame(main_frame, bg='#16213e')
        self.security_frame.pack(fill='x', pady=(20, 0))
        
        self.security_label = ttk.Label(self.security_frame, text="", style='Modern.TLabel')
        self.security_label.pack()
        
    def update_length_display(self, value):
        self.length_display.config(text=f"Caratteri: {value}")
        
    def generate_password(self):
        # Caratteri base (lettere)
        characters = string.ascii_letters
        
        # Aggiungi caratteri in base alle opzioni selezionate
        if self.include_numbers.get():
            characters += string.digits
            
        if self.include_symbols.get():
            characters += "!@#$%^&*"
            
        if self.include_special.get():
            characters += "{}[]|\\:;\"'<>,.?/"
        
        # Genera password
        length = self.length_var.get()
        password = ''.join(random.choice(characters) for _ in range(length))
        
        self.password_var.set(password)
        self.update_security_indicator(password)
        
    def update_security_indicator(self, password):
        score = 0
        feedback = []
        
        if len(password) >= 12:
            score += 1
        if any(c.isupper() for c in password):
            score += 1
        if any(c.islower() for c in password):
            score += 1
        if any(c.isdigit() for c in password):
            score += 1
        if any(c in "!@#$%^&*{}[]|\\:;\"'<>,.?/" for c in password):
            score += 1
        
        if score <= 2:
            security_text = "🔴 Sicurezza: Bassa"
            color = "#dc3545"
        elif score <= 3:
            security_text = "🟡 Sicurezza: Media"
            color = "#ffc107"
        elif score <= 4:
            security_text = "🟢 Sicurezza: Buona"
            color = "#28a745"
        else:
            security_text = "🔵 Sicurezza: Eccellente"
            color = "#00d4ff"
            
        self.security_label.config(text=security_text, foreground=color)
        
    def copy_password(self):
        password = self.password_var.get()
        if password:
            try:
                pyperclip.copy(password)
                messagebox.showinfo("Successo", "Password copiata negli appunti!")
            except:
                messagebox.showerror("Errore", "Impossibile copiare negli appunti")
        else:
            messagebox.showwarning("Attenzione", "Genera prima una password!")
            
    def clear_password(self):
        self.password_var.set("")
        self.security_label.config(text="")

def main():
    root = tk.Tk()
    app = PasswordGenerator(root)
    root.mainloop()

if __name__ == "__main__":
    main()
