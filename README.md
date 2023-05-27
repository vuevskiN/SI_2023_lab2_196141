Nikita Vuevski 196141

public class SILab2 {

    public static boolean function (User user, List<User> allUsers) {
        if (user==null || user.getPassword()==null || user.getEmail()==null){				//1
            throw new RuntimeException("Mandatory information missing!");				//2
        }

        if (user.getUsername()==null){									//3
            user.setUsername(user.getEmail());								//4
        }

        int same = 1;											//6
        if (user.getEmail().contains("@") && user.getEmail().contains(".")) {				//7
            same = 0;											//8
            for (int i=0;i<allUsers.size();i++) {							//9
                User existingUser = allUsers.get(i);							//10
                if (existingUser.getEmail() == user.getEmail()) {					//11
                    same += 1;										//12
                }
                if (existingUser.getUsername() == user.getUsername()) {					//13
                    same += 1;										//14
                }
            }
        }

        String specialCharacters="!#$%&'()*+,-./:;<=>?@[]^_`{|}";					//15
        String password = user.getPassword();								//16
        String passwordLower = password.toLowerCase();							//17

        if (passwordLower.contains(user.getUsername().toLowerCase()) || password.length()<8) {		//18
            return false;										//19
        }
        else {
            if (!passwordLower.contains(" ")) {								//20
                for (int i = 0; i < specialCharacters.length(); i++) {					//21
                    if (password.contains(String.valueOf(specialCharacters.charAt(i)))) {		//22
                        return same == 0;								//23
                    }
                }																					
            }																						
        }																							
        return false;											//24													
    }													//25											//25																						

}


[controlflowgraph](cfGraph.png)

3. Ciklonatskata kompleksnost ja dobiv so broenje na regionite. koi ispadnaa da bidat 11.

4. Vkupno ima 5 slucaevi. 
- Koga imame ist mail i razlicen username vo allUsers so sporedba so user.
- Koga user e null.
- Koga nite eden od mejlovite i username se sovpagjaat so toj od user.
- Koga imame specialCharacter vo user.password.
-Koga nemame specialCharacter vo user.password.
Ima greshka vo kodot. grankite 3-4 i 4-7. nema mikogash da se izvrshat. bidejki pred niv ima throw uslov. 
5. Multiple Condition za: p, q, r

when p is T. result is T
when p is N but q is T. result is T
when both p and q are N. result is r
