import pygame
import random

# Inisialisasi Pygame
pygame.init()

# Ukuran layar
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Village Conqueror")

# Warna
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)
BROWN = (139, 69, 19)
GOLD = (255, 215, 0)  # Warna emas untuk Gold Mine

# Font
font = pygame.font.SysFont(None, 36)

# Variabel sumber daya
gold = 100
elixir = 50
gold_rate = 1
elixir_rate = 1

# Bangunan
buildings = [
    {"name": "Gold Mine", "x": 100, "y": 150, "color": GOLD, "rate": 1, "cost": 50},
    {"name": "Elixir Collector", "x": 300, "y": 150, "color": BLUE, "rate": 1, "cost": 50},
]

# Fungsi menggambar teks
def draw_text(text, x, y, color):
    screen_text = font.render(text, True, color)
    screen.blit(screen_text, (x, y))

# Fungsi menggambar bangunan
def draw_buildings():
    for building in buildings:
        pygame.draw.rect(screen, building["color"], (building["x"], building["y"], 100, 100))
        draw_text(building["name"], building["x"] + 5, building["y"] + 105, BLACK)

# Game loop
running = True
last_update_time = pygame.time.get_ticks()

while running:
    screen.fill(WHITE)

    # Event handler
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Menghitung waktu yang telah berlalu sejak game dimulai
    current_time = pygame.time.get_ticks()
    if current_time - last_update_time > 1000:  # 1000 ms = 1 detik
        # Tambahkan sumber daya setiap detik
        gold += gold_rate
        elixir += elixir_rate
        last_update_time = current_time  # Reset waktu pembaruan

    # Gambar sumber daya
    draw_text(f"Gold: {gold}", 10, 10, BLACK)
    draw_text(f"Elixir: {elixir}", 10, 50, BLACK)

    # Gambar bangunan
    draw_buildings()

    pygame.display.flip()

pygame.quit()
