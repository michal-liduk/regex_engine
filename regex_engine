def match_char(regex, char):
    """Compares single characters. Taking into account the '.'
    wildcard"""
    return regex == '' or char == regex or (regex == '.' and char != '')

def match_char_without_wildcard(regex, char):
    return regex == "" or char == re


def match_string(regex, string):
    """Compares strings of the same length. Handles also special
    characters as '?', '*' or '+'"""
    if regex == '' or (regex == '$' and string == ''):
        return True
    elif string == '':
        return False
    elif len(regex) > 2 and regex[0] == '\\' and regex[1] == '\\':
        return match_char_without_wildcard(regex[2], string)
    elif regex[0] == "\\":
        return match_char(regex[1], string[0])
        
    elif len(regex) > 1 and regex[1] in '*?+':
        if regex[1] in '?*' and match_string(regex[2:], string):
            return True
        """using the
         recursion to call itself **inside the condition!!**"""
        elif match_char(regex[0], string[0]) and \
                ((regex[1] in '?+' and match_string(regex[2:], string[1:])) or
                    (regex[1] in '*+' and match_string(regex, string[1:]))):
            return True
    elif not match_char(regex[0], string[0]):
        return False

    return match_string(regex[1:], string[1:])


def find_match(regex, long_string):
    """Looks for matches in a longer string (than the regex)"""
    if regex == '':
        return True
    if regex[0] == '^':
        return match_string(regex[1:], long_string)

    if match_string(regex, long_string):
        return True
    elif long_string:
        return find_match(regex, long_string[1:])
    else:
        return False


def main_func():
    """Main function to get the input strings"""
    print(find_match(*input().split('|')))


if __name__ == "__main__":
    main_func()
