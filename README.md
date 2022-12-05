# Projeto-PI

Este é o canal para envio do código de projeto PI do grupo 9

import java.util.InputMismatchException;
import java.util.NoSuchElementException;
import java.util.Scanner;

public class Main {

	static int rodada = 1;
	static String opcaoMenu = "0";
	static Scanner sc = new Scanner(System.in);
	static boolean verificaEntrada = true;
	static String nomeJogador1;
	static String nomeJogador2;
	static int[] baralho = { 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

	public static void main(String[] args) {
		System.out.println("Bem vindo ao Jogo do 21! ");

		do {

			// Aqui o código usa métodos para mostrar o menu do jogo e direcionar o
			// andamento do jogo.

			mostrarMenu();

			opcaoMenu = sc.next();

			menuEscolha(opcaoMenu);

		} while (!opcaoMenu.equals("2") && !opcaoMenu.equals("4"));

		// Caso escolha a função JOGAR, será redirecionado para o game a seguir:

		if (opcaoMenu.equals("2")) {

			dialogo();

			System.out.println("\nNome do Jogador 1: ");
			nomeJogador1 = capturaEscrita(new Scanner(System.in));

			System.out.println("\nNome do Jogador 2: ");
			nomeJogador2 = capturaEscrita(new Scanner(System.in));

			iniciaJogo();

		}

	}

	// Método responsável por apresentar o menu.

	public static void mostrarMenu() {

		System.out.println("\nEscolha a opção que deseja seguir:");
		System.out.println("1 - Instruções");
		System.out.println("2 - Jogar");
		System.out.println("3 - Créditos");
		System.out.println("4 - Sair");

	}

	// Método responsável pelas respostas do menu.

	public static void menuEscolha(String a) {

		switch (a) {
		case "1":
			System.out.println("Instruções: ");
			System.out.println(
					"O \"jogo\" consiste em uma partida multiplayer do jogo de cartas 21, onde o baralho é apenas numérico e percorre de 1 à 10. \r\n"
							+ "O objetivo do jogo é chegar na somatória de 21 pontos, ou o mais próximo se comparado ao seu adversário.\r\n"
							+ "Caso a somatória dos jogadores sejam maior do que 21 pontos, o jogador com o menor saldo irá vencer a rodada.\r\n"
							+ "As cartas serão distrubuídas de maneira alternada, onde o jogador escolhe se quer virar uma nova carta ou passar a vez.\r\n"
							+ "Caso apenas um jogador passe, o jogo continuará. Caso ambos os jogadores passem, a rodada será encerrada e o vencedor, anunciado!\r\n"
							+ "Cada player começa o jogo com um barra de vida em \"100%\", a cada rodada perdida 20% será subtraído e caso chegue a zero, o jogador foi derrotado. ");
			break;
		case "2":
			System.out.println("Você escolheu JOGAR!\n");
			break;
		case "3":
			System.out.println("Baseado no mini-game da DLC de Resident Evil 7 desenvolvido pela Capcom.\r\n" + "\r"
					+ "Jogo desenvolvido por: João Victor Santos, Jonas Kendy, Kelvin Oliveira, Lucas Assis e Lucas Freire.\r\n"
					+ "\r" + "Orientador: Galvez Gonçalvez.\r" + "\r"
					+ "Senac Santo Amaro - Curso: Análise e Desenvolvimento de Sistemas \r" + "Turma C - Noturno");
			break;
		case "4":
			System.out.println("Você escolheu sair!");
			System.out.println("\n");
			System.out.println("Fim do programa");
			break;
		default:
			System.out.println("Opção Inválida!");

		}

	}

	// Método que executa o jogo

	public static void iniciaJogo() {

		int lifeJ1 = 100;
		int lifeJ2 = 100;

		while (lifeJ1 > 0 && lifeJ2 > 0) {

			int cartaJ1 = 0;
			int somaJ1 = 0;
			int cartaJ2 = 0;
			int somaJ2 = 0;
			int resp1 = 1;
			int resp2 = 1;
			boolean receberCard1 = false;
			boolean receberCard2 = false;

			System.out.println("------------");
			System.out.println("/ Rodada " + rodada + " /");
			System.out.println("------------");
			System.out.println("\n");

			do {

				// Aqui o código randomiza as cartas e alimenta a variável de soma, e imprime o
				// saldo.

				if (resp1 == 1) {
					cartaJ1 = baralho[(int) (Math.random() * baralho.length)];
					somaJ1 = somaJ1 + cartaJ1;
					System.out.println(nomeJogador1 + " : você recebeu uma carta " + cartaJ1);
					System.out.println(nomeJogador1 + " : o saldo atual é " + somaJ1);

				}

				if (resp2 == 1) {
					cartaJ2 = baralho[(int) (Math.random() * baralho.length)];
					somaJ2 = somaJ2 + cartaJ2;
					System.out.println(nomeJogador2 + " : você recebeu uma carta " + cartaJ2);
					System.out.println(nomeJogador2 + " : o saldo atual é " + somaJ2);

				}

				if (somaJ1 <= 20 && resp1 == 1) {

					verificaEntrada = true;

					while (verificaEntrada) {
						System.out.println("\n" + nomeJogador1
								+ " : deseja receber mais uma carta? *Homem Misterioso*\n1 - Sim\n2 - Não");
						resp1 = capturaInteiros(new Scanner(System.in));
					}

				}
				if (resp1 == 2 || somaJ1 > 20) {
					receberCard1 = true;

				}
				if (somaJ2 <= 20 && resp2 == 1) {

					verificaEntrada = true;

					while (verificaEntrada) {

						System.out.println("\n" + nomeJogador2
								+ " : deseja receber mais uma carta? *Homem Misterioso*\n1 - Sim\n2 - Não");
						resp2 = capturaInteiros(new Scanner(System.in));
					}

				}
				if (resp2 == 2 || somaJ2 > 20) {
					receberCard2 = true;

				}
			} while (receberCard1 == false || receberCard2 == false);

			// Validação do vencedor da rodada

			System.out.println("\n");
			System.out.println("Saldo " + nomeJogador1 + " : " + somaJ1);
			System.out.println("\n");
			System.out.println("Saldo " + nomeJogador2 + " : " + somaJ2);
			System.out.println("\n");

			if (somaJ1 == somaJ2) {

				System.out.println("\n");
				System.out.println("********");
				System.out.println("*Empate*");
				System.out.println("********");
				System.out.println("\n");
				rodada++;

			}
			if (somaJ1 < 22 && somaJ2 < somaJ1) {
				System.out.println("\n");
				System.out.println("*******************");
				System.out.println("* " + nomeJogador1 + " ganhou!");
				System.out.println("*******************");
				System.out.println("\n");
				rodada++;
				lifeJ2 = lifeJ2 - 20;
			}
			if (somaJ1 > 21 && somaJ2 > somaJ1) {
				System.out.println("\n");
				System.out.println("*******************");
				System.out.println("* " + nomeJogador1 + " ganhou!");
				System.out.println("*******************");
				System.out.println("\n");
				rodada++;
				lifeJ2 = lifeJ2 - 20;
			}
			if (somaJ2 > 21 && somaJ1 <= 21) {
				System.out.println("\n");
				System.out.println("*******************");
				System.out.println("* " + nomeJogador1 + " ganhou!");
				System.out.println("*******************");
				System.out.println("\n");
				rodada++;
				lifeJ2 = lifeJ2 - 20;
			}
			if (somaJ2 < 22 && somaJ1 < somaJ2) {
				System.out.println("\n");
				System.out.println("*******************");
				System.out.println("* " + nomeJogador2 + " ganhou!");
				System.out.println("*******************");
				System.out.println("\n");
				rodada++;
				lifeJ1 = lifeJ1 - 20;
			}
			if (somaJ1 > 21 && somaJ2 <= 21) {
				System.out.println("\n");
				System.out.println("*******************");
				System.out.println("* " + nomeJogador2 + " ganhou!");
				System.out.println("*******************");
				System.out.println("\n");
				rodada++;
				lifeJ1 = lifeJ1 - 20;
			}
			if (somaJ2 > 21 && somaJ1 > somaJ2) {
				System.out.println("\n");
				System.out.println("*******************");
				System.out.println("* " + nomeJogador2 + " ganhou!");
				System.out.println("*******************");
				System.out.println("\n");
				rodada++;
				lifeJ1 = lifeJ1 - 20;
			}

			System.out.println("\n");
			System.out.println("----------------------------------");
			System.out.println("Pontos de Vida - " + nomeJogador1 + " : " + lifeJ1 + "%");
			System.out.println("----------------------------------");
			System.out.println("Pontos de Vida - " + nomeJogador2 + " : " + lifeJ2 + "%");
			System.out.println("----------------------------------");
			System.out.println("\n");

		}

		// Regra para o vencedor da partida ser impresso na tela

		if (lifeJ1 > 0) {
			System.out.println("\n");
			System.out.println("O vencedor foi " + nomeJogador1 + " ! ");
			System.out.println("\nFIM");
		}
		if (lifeJ2 > 0) {
			System.out.println("\n");
			System.out.println("O vencedor foi " + nomeJogador2 + " ! ");
			System.out.println("\nFIM");
			sc.close();
		}
	}

	// Método que faz o recebimento dos nomes dos jogadores

	public static String capturaEscrita(Scanner sc) {

		String entrada = "";

		try {

			entrada = sc.nextLine();
			verificaEntrada = false;

		} catch (InputMismatchException ex) {

			System.out.println("Não inserir caracteres especiais! ");
		}

		return entrada;

	}

	// Método por capturar a entrada dos jogadores durante as rodadas
	public static int capturaInteiros(Scanner sc) {

		int resposta = 0;

		try {

			resposta = sc.nextInt();
			verificaEntrada = false;

		} catch (InputMismatchException ex) {

			System.out.println("Por favor inserir apenas números! ");

		} catch (NoSuchElementException ex) {

			System.out.println("Por favor inserir apenas números! ");

		}

		return resposta;
	}

	// Diálogo de introdução ao jogo
	public static void dialogo() {

		System.out.println("Começou!!");
		System.out.println("\nVocê estava andando calmamente na rua e é abordado por um homem suspeito.\n"
				+ "Ele te convida para tomar um drink e te oferece um trabalho, você está desempregado.\n"
				+ "Seu trabalho atual é horrível, está te deixando maluco, então decide aceitar a proposta.\n"
				+ "Após algumas horas de conversa, você começa a se sentir estranho e logo desamaia.\n"
				+ "Quando você acorda, você percebe que na sua frente tem uma pessoa que aparenta estar com medo.\n"
				+ "Você escuta uma voz próxima: *Olá jogadores sejam bem vindos ao Jogo 21 !*\n"
				+ "*Participantes, identifiquem-se!*\n");

	}

}

