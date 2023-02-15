# taos api

## Setup
Install packages  
`pip3 install -r requirements.txt`  

Make migrations and run server  
`python3 manage.py migrate`   
`python3 manage.py runserver`   

To run tests    
`python3 manage.py test`    
## Important API Functions

### Create Accounting Firm
URL:`/api/accounting_firms/`    
Method: POST    
Data:   
`{"name": "New Firm"}`
Response:   
`{'id': 1, 'name': 'New Firm'}`   

### Create User/Client
URL:`/api/users/`    
Method: POST    
Data:   
`{"name": "New User"}`
Response:   
`{'id': 1, 'name': 'New User'}`   

### Create TaxForm Blueprint
URL:`/api/tax_forms/`    
Method: POST    
Data:   
`{
            "name": "New Form",
            "accounting_firm": 1,
            "questions": [
                {
                    "order": 1,
                    "question_text": "Test Question 1",
                    "question_type": "TX",
                    "options": []
                },
                {
                    "order": 2,
                    "question_text": "Test Question 2",
                    "question_type": "MC",
                    "options": [
                        {"order": 1, "option_text": "Test Option 1", "form_question": 2},
                        {"order": 2, "option_text": "Test Option 2", "form_question": 2},
                        {"order": 3, "option_text": "Test Option 3", "form_question": 2},
                        {"order": 4, "option_text": "Test Option 4", "form_question": 2},
                    ]
                },
                {
                    "order": 3,
                    "question_text": "Test Question 3",
                    "question_type": "RD",
                    "options": [
                        {"order": 1, "option_text": "Test Option 1", "form_question": 2},
                        {"order": 2, "option_text": "Test Option 2", "form_question": 2},
                        {"order": 3, "option_text": "Test Option 3", "form_question": 2},
                        {"order": 4, "option_text": "Test Option 4", "form_question": 2},
                    ]
                }
            ]
        }`
Response:   
`{'id': 1, ...}`   

### Create ClientForm from TaxForm blueprint and assign to User/Client
URL:`/api/client_forms/admin/<int:firm_id>/`    
Method: POST    
Data:   
`{"tax_form": 1,"client": 1}`   
Response:   
{id: 1, ...}    

### List all ClientForms for an AccountingFirm
URL:`/api/client_forms/admin/<int:firm_id>/`    
Method: GET    
Response:   
`{"results": [...]}`    

### List all ClientForms for a User
URL:`/api/client_forms/user/<int:user_id>/`    
Method: GET    
Response:   
`{"results": [...]}`    

### List all ClientForms for a User
URL:`/api/client_forms/user/<int:user_id>/`    
Method: GET    
Response:   
`{"results": [...]}`    

### Submit ClientForm as a User
URL:`/api/client_forms/user/<int:user_id>/<int:form_id>/`    
Method: PUT    
Data:   
`{"id": 2,
            "questions": [
                {
                    "id": 1,
                    "order": 1,
                    "question_text": "Test Question 1",
                    "question_type": "TX",
                    "options": [],
                    "answer_text": "..."
                },
                {
                    "id": 2,
                    "order": 2,
                    "question_text": "Test Question 2",
                    "question_type": "MC",
                    "options": [],
                    "answer_text": "..."
                },
                {
                    "id": 3,
                    "order": 3,
                    "question_text": "Test Question 3",
                    "question_type": "RD",
                    "options": [],
                    "answer_text": "..."                  
                }
            ]
        }`    
Response:
`{"id": 1, ...}`    
