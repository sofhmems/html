import pygame as pg
import random
import os


branco = (255, 255, 255)
preto = (0, 0, 0)
vermelho = (255, 0, 0)
verde = (0, 255, 0)
giz = (255, 255, 255)  


pg.init()
window = pg.display.set_mode((1000, 600))
pg.display.set_caption("Jogo da Forca")


background_path = "blackboard.jpg"


if os.path.exists(background_path):
    background = pg.image.load(background_path)
    background = pg.transform.scale(background, (1000, 600))
else:
    background = None


pg.font.init()
fonte = pg.font.SysFont("Comic Sans MS", 50)
fonte_rb = pg.font.SysFont("Comic Sans MS", 30)


conjuntos = {
    'ANIMAIS': ['PARALELEPIPEDO', 'ORNITORINCO', 'APARTAMENTO'],
    'FRUTAS': ['MORANGO', 'BANANA', 'ABACAXI'],
    'OBJETOS': ['CADEIRA', 'MESA', 'COMPUTADOR']
}


categoria_escolhida = random.choice(list(conjuntos.keys()))
palavras = conjuntos[categoria_escolhida]

tentativas_de_letras = [' ', '-']
palavra_escolhida = ''
palavra_camuflada = ''
end_game = True
chance = 0
letra = ' '
click_last_status = False
game_started = False
game_over = False
mensagem = ''
jogar_novamente = False

def Tela_Inicial(window):
    if background:
        window.blit(background, (0, 0))
    else:
        window.fill(preto)
    pg.draw.rect(window, giz, (350, 250, 300, 100))
    texto = fonte_rb.render('INICIAR JOGO', 1, preto)
    window.blit(texto, (400, 280))
    pg.display.update()

def Desenho_da_Forca(window, chance):
    if background:
        window.blit(background, (0, 0))
    else:
        window.fill(preto)
    pg.draw.line(window, giz, (100, 500), (100, 100), 10)  # Forca vertical
    pg.draw.line(window, giz, (50, 500), (150, 500), 10)   # Base
    pg.draw.line(window, giz, (100, 100), (300, 100), 10)  # Forca horizontal
    pg.draw.line(window, giz, (300, 100), (300, 150), 10)  # Corda
    if chance >= 1:
        # Cabeça
        pg.draw.circle(window, giz, (300, 200), 50, 10)
    if chance >= 2:
        # Olho Esquerdo
        pg.draw.circle(window, giz, (280, 190), 5, 5)
    if chance >= 3:
        # Olho Direito
        pg.draw.circle(window, giz, (320, 190), 5, 5)
    if chance >= 4:
        # Boca
        pg.draw.line(window, giz, (285, 220), (315, 220), 5)
    if chance >= 5:
        # Tronco
        pg.draw.line(window, giz, (300, 250), (300, 350), 10)
    if chance >= 6:
        # Braço Direito
        pg.draw.line(window, giz, (300, 260), (225, 350), 10)
    if chance >= 7:
        # Braço Esquerdo
        pg.draw.line(window, giz, (300, 260), (375, 350), 10)
    if chance >= 8:
        # Perna Direita
        pg.draw.line(window, giz, (300, 350), (375, 450), 10)
    if chance >= 9:
        # Perna Esquerda
        pg.draw.line(window, giz, (300, 350), (225, 450), 10)
    if chance >= 10:
        # Desenho Completo - Você perdeu
        pass

def Desenho_Restart_Button(window):
    pg.draw.rect(window, giz, (700, 100, 200, 65))
    texto = fonte_rb.render('Restart', 1, preto)
    window.blit(texto, (740, 120))

def Sorteando_Palavra(palavras, palavra_escolhida, end_game):
    if end_game == True:
        palavra_n = random.randint(0, len(palavras) - 1)
        palavra_escolhida = palavras[palavra_n]
        end_game = False
        chance = 0
    return palavra_escolhida, end_game

def Camuflando_Palavra(palavra_escolhida, palavra_camuflada, tentativas_de_letras):
    palavra_camuflada = palavra_escolhida
    for n in range(len(palavra_camuflada)):
        if palavra_camuflada[n:n + 1] not in tentativas_de_letras:
            palavra_camuflada = palavra_camuflada.replace(palavra_camuflada[n], '#')
    return palavra_camuflada

def Tentando_uma_Letra(tentativas_de_letras, palavra_escolhida, letra, chance):
    if letra not in tentativas_de_letras:
        tentativas_de_letras.append(letra)
        if letra not in palavra_escolhida:
            chance += 1
    elif letra in tentativas_de_letras:
        pass
    return tentativas_de_letras, chance

def Palavra_do_Jogo(window, palavra_camuflada):
    palavra = fonte.render(palavra_camuflada, 1, giz)
    window.blit(palavra, (200, 500))

def Mensagem_Final(window, mensagem):
    texto = fonte.render(mensagem, 1, vermelho if "errou" in mensagem else verde)
    window.blit(texto, (300, 400))
    pg.draw.rect(window, giz, (350, 500, 300, 100))
    texto = fonte_rb.render('JOGAR NOVAMENTE', 1, preto)
    window.blit(texto, (370, 530))

def Restart_do_Jogo(palavra_camuflada, end_game, chance, letra, tentativas_de_letras, click_last_status, click, x, y):
    if click_last_status == False and click[0] == True:
        if x >= 700 and x <= 900 and y >= 100 and y <= 165:
            tentativas_de_letras = [' ', '-']
            end_game = True
            chance = 0
            letra = ' '
    return end_game, chance, tentativas_de_letras, letra

def Jogar_Novamente(window, click, x, y, click_last_status):
    jogar_novamente = False
    if click_last_status == False and click[0] == True:
        if x >= 350 and x <= 650 and y >= 500 and y <= 600:
            jogar_novamente = True
    return jogar_novamente


while True:
    for event in pg.event.get():
        if event.type == pg.QUIT:
            pg.quit()
            quit()
        if event.type == pg.KEYDOWN:
            letra = str(pg.key.name(event.key)).upper()

    
    mouse = pg.mouse.get_pos()
    mouse_position_x = mouse[0]
    mouse_position_y = mouse[1]

    
    click = pg.mouse.get_pressed()

    if not game_started:
        Tela_Inicial(window)
        if click[0] == True and 350 <= mouse_position_x <= 650 and 250 <= mouse_position_y <= 350:
            game_started = True
    else:
        if not game_over:
            
            Desenho_da_Forca(window, chance)
            Desenho_Restart_Button(window)
            palavra_escolhida, end_game = Sorteando_Palavra(palavras, palavra_escolhida, end_game)
            palavra_camuflada = Camuflando_Palavra(palavra_escolhida, palavra_camuflada, tentativas_de_letras)
            tentativas_de_letras, chance = Tentando_uma_Letra(tentativas_de_letras, palavra_escolhida, letra, chance)
            Palavra_do_Jogo(window, palavra_camuflada)
            end_game, chance, tentativas_de_letras, letra = Restart_do_Jogo(palavra_camuflada, end_game, chance, letra, tentativas_de_letras, click_last_status, click, mouse_position_x, mouse_position_y)

            
            if palavra_camuflada == palavra_escolhida:
                mensagem = 'Você acertou!'
                game_over = True
            elif chance >= 10:
                mensagem = 'Você errou!'
                game_over = True

        else:
            Mensagem_Final(window, mensagem)
            if Jogar_Novamente(window, click, mouse_position_x, mouse_position_y, click_last_status):
                
                game_over = False
                end_game = True
                tentativas_de_letras = [' ', '-']
                chance = 0
                letra = ' '
                categoria_escolhida = random.choice(list(conjuntos.keys()))
                palavras = conjuntos[categoria_escolhida]

        
        if click[0] == True:
            click_last_status = True
        else:
            click_last_status = False

    pg.display.update()
