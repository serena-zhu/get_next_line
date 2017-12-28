# **************************************************************************** #
#                                                                              #
#                                                         :::      ::::::::    #
#    Makefile                                           :+:      :+:    :+:    #
#                                                     +:+ +:+         +:+      #
#    By: yazhu <marvin@42.fr>                       +#+  +:+       +#+         #
#                                                 +#+#+#+#+#+   +#+            #
#    Created: 2017/11/27 10:32:40 by yazhu             #+#    #+#              #
#    Updated: 2017/12/18 13:37:57 by yazhu            ###   ########.fr        #
#                                                                              #
# **************************************************************************** #

NAME	= libft.a
CFILES	= ft_strcpy.c ft_strdel.c ft_strcat.c ft_bzero.c ft_strdup.c ft_strnew.c
OFILES	= $(CFILES:.c=.o)

all: $(NAME)

$(NAME):
	@gcc -Wall -Wextra -Werror -c $(CFILES)
	@ar rc $(NAME) $(OFILES)

clean:
	@/bin/rm -f $(OFILES)

fclean: clean
	@/bin/rm -f $(NAME)

re: fclean all
