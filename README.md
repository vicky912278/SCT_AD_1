import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

public class Calculator extends JFrame implements ActionListener {

    private JTextField inputField;
    private double num1, num2, result;
    private String operator;

    public Calculator() {
        setTitle(" Calculator");
        setSize(350, 450);
        setLocationRelativeTo(null);
        setDefaultCloseOperation(EXIT_ON_CLOSE);

        inputField = new JTextField();
        inputField.setFont(new Font("SansSerif", Font.BOLD, 24));
        inputField.setHorizontalAlignment(JTextField.RIGHT);
        inputField.setEditable(false);

        JPanel panel = new JPanel(new GridLayout(5, 4, 5, 5));
        String[] buttons = {
                "7", "8", "9", "/",
                "4", "5", "6", "*",
                "1", "2", "3", "-",
                "0", ".", "=", "+",
                "C", "Exit"
        };

        for (String text : buttons) {
            JButton button = new JButton(text);
            button.setFont(new Font("SansSerif", Font.BOLD, 18));
            button.addActionListener(this);
            panel.add(button);
        }

        add(inputField, BorderLayout.NORTH);
        add(panel, BorderLayout.CENTER);
        setVisible(true);
    }

    public void actionPerformed(ActionEvent e) {
        String cmd = e.getActionCommand();

        try {
            switch (cmd) {
                case "C":
                    inputField.setText("");
                    break;
                case "Exit":
                    System.exit(0);
                    break;
                case "+": case "-": case "*": case "/":
                    num1 = Double.parseDouble(inputField.getText());
                    operator = cmd;
                    inputField.setText("");
                    break;
                case "=":
                    num2 = Double.parseDouble(inputField.getText());
                    switch (operator) {
                        case "+": result = num1 + num2; break;
                        case "-": result = num1 - num2; break;
                        case "*": result = num1 * num2; break;
                        case "/":
                            if (num2 == 0) {
                                inputField.setText("Error: /0");
                                return;
                            }
                            result = num1 / num2; break;
                    }
                    inputField.setText(String.valueOf(result));
                    break;
                default:
                    inputField.setText(inputField.getText() + cmd);
            }
        } catch (Exception ex) {
            inputField.setText("Error");
        }
    }

    public static void main(String[] args) {
        new Calculator();
    }
}

