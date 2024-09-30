namespace ValidationTask

{

    internal class Program

    {

        static void Main(string[] args)

        {
            string firstName;
            string lastName;
            string username;
            string password;
            string emailAddress;
            int age;

            // get the user inputs until all are valid.

            // The username should only be output once

            Console.WriteLine("Enter first name: ");
            firstName = Console.ReadLine();
            Console.WriteLine("Enter last name: ");
            lastName = Console.ReadLine();
            while (Convert.ToBoolean(ValidName(firstName, lastName)) == false)
            {
                Console.WriteLine("Enter first name: ");
                firstName = Console.ReadLine();
                Console.WriteLine("Enter last name: ");
                lastName = Console.ReadLine();
            }
            Console.WriteLine("Enter age: ");
            age = Convert.ToInt32(Console.ReadLine());
            while (Convert.ToBoolean(ValidAge(age)) == false)
            {
                Console.WriteLine("Enter age: ");
                age = Convert.ToInt32(Console.ReadLine());
            }
            Console.WriteLine("Enter Password: ");
            password = Console.ReadLine();
            while (Convert.ToBoolean(ValidPassword(password)) == false)
            {
                Console.WriteLine("Enter Password: ");
                password = Console.ReadLine();
            }
            Console.WriteLine("Enter email address: ");
            emailAddress = Console.ReadLine();
            while (Convert.ToBoolean(validEmail(emailAddress)) == false)
            {
                Console.WriteLine("Enter email address: ");
                emailAddress = Console.ReadLine();
            }
            username = createUserName(firstName, lastName, age);
            Console.WriteLine("Username is " + username + " , you have successfully registered please remember your password");
        }

        static bool ValidName(string firstName, string lastName)
        {
            int firstLength = firstName.Length;
            int lastLength = lastName.Length;
            if (firstLength >= 2 && lastLength >= 2)
            {
                for (int i = 0; i < firstLength; i++)
                {
                    if (char.IsLetter(firstName[i]))
                    {
                    }
                    else
                    {
                        return false;
                    }
                }
                for (int i = 0; i < lastLength; i++)
                {
                    if (char.IsLetter(lastName[i]))
                    {
                    }
                    else
                    {
                        return false;
                    }
                }
                return true;
            }
            return false;
        }
        static bool ValidAge(int age)
        {
            if (age >= 11 && age <= 18)
            {
                return true;
            }
            return false;
        }
        static bool ValidPassword(string password)
        {
            //This is cheecking every possibilty that it can be and thus it is making itself very large
            if (password.Length >= 8)
            {
                for (int i = 0; i < password.Length; i++)
                {
                    if (char.IsLower(password[i]))
                    {
                        for (int j = 0; j < password.Length; j++)
                        {
                            if (char.IsDigit(password[j]))
                            {
                                for (int k = 0; k < password.Length; k++)
                                {
                                    if (char.IsUpper(password[k]))
                                    {
                                        for (int l = 0; l < password.Length; l++)
                                        {
                                            if (char.IsSymbol(password[l]) || password[l] == '!' || password[l] == '+')
                                            {
                                                for (int m = 0; m < password.Length - 2; m++)
                                                {
                                                    password = password.ToLower();
                                                    if (((Convert.ToInt32((password[m])) + 2) == (Convert.ToInt32(password[m + 1])) + 1))
                                                    {
                                                        if (((Convert.ToInt32(password[m]) + 2) == (Convert.ToInt32(password[m + 2]))))// this ends up checking everything and it works for most things but there are somethings that it wont work for
                                                        {
                                                            return false;
                                                        }
                                                    }
                                                    if ((Convert.ToInt32(password[m]) - 2) == (Convert.ToInt32(password[m + 1]) - 1))
                                                    {
                                                        if ((Convert.ToInt32(password[m]) - 2) == Convert.ToInt32(password[m + 2]))
                                                        {
                                                            return false;
                                                        }
                                                    }
                                                    if (Convert.ToInt32(password[m]) == Convert.ToInt32(password[m + 1]))
                                                    {
                                                        if (Convert.ToInt32(password[m]) == Convert.ToInt32(password[m + 2]))

                                                        {
                                                            return false;
                                                        }
                                                    }
                                                }
                                                return true;
                                            }
                                        }
                                        return false;
                                    }
                                }
                                return false;
                            }
                        }
                        return false;
                    }
                }
                return false;
            }
            return false;
        }
        static bool validEmail(string email)

        {
            if (email.IndexOf('@') >= 3)
            {
                if (email.IndexOf('.') >= email.IndexOf('@') + 3)
                {
                    if (email.Length >= email.IndexOf('.') + 2)
                    {
                        return true;
                    }
                    return false;
                }
                return false;
            }
            return false;
        }
        static string createUserName(string firstName, string lastName, int age)
        {
            Console.WriteLine("Enter your username: ");
            string username = Console.ReadLine();
            while (username != (firstName.Substring(0, 2) + lastName.Substring((lastName.Length) - 2, 2) + Convert.ToString(age)))
            {
                Console.WriteLine("Enter your username: ");
                username = Console.ReadLine();
            }
            return username;
            // this was just a really simple way of getting it to send back fast
        }
    }
}
