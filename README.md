import javax.swing.*;
import java.awt.*;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;

public class MarksCalculatorGUI extends JFrame {

    private JTextField[] subjectFields;
    private JLabel totalMarksLabel;
    private JLabel averagePercentageLabel;
    private JLabel gradeLabel;
    private final int NUMBER_OF_SUBJECTS = 5;

    public MarksCalculatorGUI() {
        setTitle("Marks Calculator");
        setSize(400, 300);
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        setLayout(new GridLayout(NUMBER_OF_SUBJECTS + 4, 2));

        subjectFields = new JTextField[NUMBER_OF_SUBJECTS];
        for (int i = 0; i < NUMBER_OF_SUBJECTS; i++) {
            add(new JLabel("Subject " + (i + 1) + " Marks:"));
            subjectFields[i] = new JTextField();
            add(subjectFields[i]);
        }

        JButton calculateButton = new JButton("Calculate");
        calculateButton.addActionListener(new CalculateButtonListener());
        add(calculateButton);

        totalMarksLabel = new JLabel("Total Marks:");
        add(totalMarksLabel);

        averagePercentageLabel = new JLabel("Average Percentage:");
        add(averagePercentageLabel);

        gradeLabel = new JLabel("Grade:");
        add(gradeLabel);

        setVisible(true);
    }

    private class CalculateButtonListener implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            try {
                int totalMarks = 0;
                for (JTextField subjectField : subjectFields) {
                    totalMarks += Integer.parseInt(subjectField.getText());
                }
                int averagePercentage = totalMarks / NUMBER_OF_SUBJECTS;
                String grade = calculateGrade(averagePercentage);

                totalMarksLabel.setText("Total Marks: " + totalMarks);
                averagePercentageLabel.setText("Average Percentage: " + averagePercentage + "%");
                gradeLabel.setText("Grade: " + grade);
            } catch (NumberFormatException ex) {
                JOptionPane.showMessageDialog(null, "Please enter valid marks for all subjects.", "Input Error", JOptionPane.ERROR_MESSAGE);
            }
        }

        private String calculateGrade(int averagePercentage) {
            if (averagePercentage >= 90) {
                return "A+";
            } else if (averagePercentage >= 80) {
                return "A";
            } else if (averagePercentage >= 70) {
                return "B+";
            } else if (averagePercentage >= 60) {
                return "B";
            } else if (averagePercentage >= 50) {
                return "C+";
            } else if (averagePercentage >= 40) {
                return "C";
            } else {
                return "F";
            }
        }
    }

    public static void main(String[] args) {
        SwingUtilities.invokeLater(MarksCalculatorGUI::new);
    }
}
